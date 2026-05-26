# Worked Answers

Use this file after attempting an exercise. These are not the only valid
solutions. They are comparison answers that show the expected shape, tradeoffs,
and tests.

The answers favor clarity over completeness. If a solution starts becoming a
framework, stop and record the friction instead.

## 001_ownership_basics

Expected shape:

- owned world state,
- borrowed read-only access for inspection,
- borrowed mutable access for controlled updates,
- no long-lived references between domain objects.

Worked answer:

```rust
#[derive(Debug, Clone, PartialEq, Eq)]
struct Good {
    name: String,
}

#[derive(Debug, Clone, Copy, PartialEq, Eq, Hash)]
struct GoodId(usize);

#[derive(Debug, Default)]
struct Catalog {
    goods: Vec<Good>,
}

impl Catalog {
    fn add_good(&mut self, name: impl Into<String>) -> GoodId {
        let id = GoodId(self.goods.len());
        self.goods.push(Good { name: name.into() });
        id
    }

    fn get(&self, id: GoodId) -> Option<&Good> {
        self.goods.get(id.0)
    }
}

#[test]
fn good_id_points_to_owned_catalog_data() {
    let mut catalog = Catalog::default();
    let fuel = catalog.add_good("Fuel");

    assert_eq!(catalog.get(fuel).unwrap().name, "Fuel");
}
```

Comparison notes:

- `Catalog` owns the goods.
- `GoodId` is copyable and can be stored freely.
- Consumers borrow from `Catalog` only when reading.
- This avoids a web of references between entities.

Common acceptable variation:

- Use `u32` instead of `usize` for IDs if serialization stability matters.

## 002_structs_and_enums

Expected shape:

- newtypes for domain quantities,
- enums for finite state,
- tests for invalid transitions.

Worked answer:

```rust
#[derive(Debug, Clone, Copy, PartialEq, Eq)]
struct Credits(i64);

#[derive(Debug, Clone, Copy, PartialEq, Eq)]
struct Quantity(u32);

#[derive(Debug, Clone, Copy, PartialEq, Eq, Hash)]
struct MarketId(u32);

#[derive(Debug, Clone, Copy, PartialEq, Eq)]
enum OrderState {
    Open,
    Filled,
    Cancelled,
}

#[derive(Debug, Clone, PartialEq, Eq)]
struct Order {
    market: MarketId,
    quantity: Quantity,
    limit_price: Credits,
    state: OrderState,
}

impl Order {
    fn new(market: MarketId, quantity: Quantity, limit_price: Credits) -> Self {
        Self {
            market,
            quantity,
            limit_price,
            state: OrderState::Open,
        }
    }

    fn fill(&mut self) -> Result<(), &'static str> {
        match self.state {
            OrderState::Open => {
                self.state = OrderState::Filled;
                Ok(())
            }
            OrderState::Filled => Err("order already filled"),
            OrderState::Cancelled => Err("cancelled order cannot be filled"),
        }
    }

    fn cancel(&mut self) -> Result<(), &'static str> {
        match self.state {
            OrderState::Open => {
                self.state = OrderState::Cancelled;
                Ok(())
            }
            OrderState::Filled => Err("filled order cannot be cancelled"),
            OrderState::Cancelled => Err("order already cancelled"),
        }
    }
}

#[test]
fn cancelled_order_cannot_be_filled() {
    let mut order = Order::new(MarketId(1), Quantity(10), Credits(50));

    order.cancel().unwrap();

    assert!(order.fill().is_err());
    assert_eq!(order.state, OrderState::Cancelled);
}
```

Comparison notes:

- `OrderState` replaces string states.
- The transition rules are explicit and testable.
- This is better than a trait hierarchy for early domain modeling.

## 003_tick_loop

Expected shape:

- fixed tick counter,
- deterministic update function,
- no wall-clock time,
- no IO.

Worked answer:

```rust
#[derive(Debug, Clone, PartialEq, Eq)]
struct Market {
    supply: i32,
    demand: i32,
    price: i32,
}

#[derive(Debug, Clone, PartialEq, Eq)]
struct World {
    tick: u64,
    markets: Vec<Market>,
}

impl World {
    fn step(&mut self) {
        self.tick += 1;

        for market in &mut self.markets {
            let pressure = market.demand - market.supply;
            market.price = (market.price + pressure.signum()).max(1);
        }
    }
}

#[test]
fn fixed_tick_is_deterministic() {
    let initial = World {
        tick: 0,
        markets: vec![Market {
            supply: 8,
            demand: 10,
            price: 100,
        }],
    };

    let mut a = initial.clone();
    let mut b = initial;

    for _ in 0..5 {
        a.step();
        b.step();
    }

    assert_eq!(a, b);
    assert_eq!(a.tick, 5);
    assert_eq!(a.markets[0].price, 105);
}
```

Comparison notes:

- `step` is deterministic because it depends only on state.
- The algorithm is deliberately simple.
- Any randomness should be explicit and seeded later.

## 004_serialization

Expected shape:

- serializable state,
- round-trip test,
- persistence outside tick logic.

Worked answer:

```rust
use serde::{Deserialize, Serialize};

#[derive(Debug, Clone, PartialEq, Eq, Serialize, Deserialize)]
struct World {
    tick: u64,
    markets: Vec<Market>,
}

#[derive(Debug, Clone, PartialEq, Eq, Serialize, Deserialize)]
struct Market {
    supply: i32,
    demand: i32,
    price: i32,
}

#[test]
fn world_round_trips_through_json() {
    let world = World {
        tick: 3,
        markets: vec![Market {
            supply: 8,
            demand: 10,
            price: 103,
        }],
    };

    let encoded = serde_json::to_string_pretty(&world).unwrap();
    let decoded: World = serde_json::from_str(&encoded).unwrap();

    assert_eq!(decoded, world);
}
```

Comparison notes:

- `serde_json` is readable and good for early learning.
- Do not optimize into `bincode` until format size matters.
- Do not serialize caches unless replay requires them.

## 005_replay_testing

Expected shape:

- commands are inputs,
- events are outputs,
- replay rebuilds state from seed plus commands.

Worked answer:

```rust
#[derive(Debug, Clone, PartialEq, Eq)]
enum Command {
    SetDemand { market: usize, demand: i32 },
    SetSupply { market: usize, supply: i32 },
    Tick,
}

#[derive(Debug, Clone, PartialEq, Eq)]
enum Event {
    DemandSet { market: usize, demand: i32 },
    SupplySet { market: usize, supply: i32 },
    TickAdvanced { tick: u64 },
}

fn apply(world: &mut World, command: &Command) -> Vec<Event> {
    match *command {
        Command::SetDemand { market, demand } => {
            world.markets[market].demand = demand;
            vec![Event::DemandSet { market, demand }]
        }
        Command::SetSupply { market, supply } => {
            world.markets[market].supply = supply;
            vec![Event::SupplySet { market, supply }]
        }
        Command::Tick => {
            world.step();
            vec![Event::TickAdvanced { tick: world.tick }]
        }
    }
}

fn replay(initial: World, commands: &[Command]) -> (World, Vec<Event>) {
    let mut world = initial;
    let mut events = Vec::new();

    for command in commands {
        events.extend(apply(&mut world, command));
    }

    (world, events)
}

#[test]
fn same_commands_replay_to_same_state() {
    let initial = World {
        tick: 0,
        markets: vec![Market {
            supply: 10,
            demand: 10,
            price: 100,
        }],
    };

    let commands = vec![
        Command::SetDemand {
            market: 0,
            demand: 12,
        },
        Command::Tick,
        Command::Tick,
    ];

    let (a, events_a) = replay(initial.clone(), &commands);
    let (b, events_b) = replay(initial, &commands);

    assert_eq!(a, b);
    assert_eq!(events_a, events_b);
    assert_eq!(a.markets[0].price, 102);
}
```

Comparison notes:

- Events describe what happened; commands drive behavior.
- Replay should not depend on Godot, networking, or wall-clock time.
- If event order changes unexpectedly, a replay test should catch it.

## 006_traits_boundaries

Expected answer shape:

- implement the concrete version first,
- introduce a trait only for a real boundary,
- compare concrete, generic, and `dyn Trait` versions in notes.

Minimal worked boundary:

```rust
trait SnapshotStore {
    type Error;

    fn save(&mut self, name: &str, world: &World) -> Result<(), Self::Error>;
    fn load(&self, name: &str) -> Result<Option<World>, Self::Error>;
}
```

Good comparison conclusion:

- Keep simulation logic concrete.
- Use traits at IO/storage/integration boundaries.
- Avoid trait objects for core domain entities unless the exercise proves the
  need.

## 007_error_handling

Expected answer shape:

- domain errors are typed,
- prototype/tool errors may use `anyhow`,
- library-like boundaries should avoid string errors.

Worked answer:

```rust
#[derive(Debug, PartialEq, Eq)]
enum SimError {
    UnknownMarket(usize),
    InvalidQuantity,
}

fn set_demand(world: &mut World, market: usize, demand: i32) -> Result<(), SimError> {
    if demand < 0 {
        return Err(SimError::InvalidQuantity);
    }

    let market = world
        .markets
        .get_mut(market)
        .ok_or(SimError::UnknownMarket(market))?;

    market.demand = demand;
    Ok(())
}
```

Comparison notes:

- The caller can match on error type.
- The error is part of the command boundary contract.

## 008_modules_and_crates

Expected answer shape:

```text
src/
  lib.rs
  model.rs
  sim.rs
  replay.rs
```

Worked `lib.rs` shape:

```rust
mod model;
mod replay;
mod sim;

pub use model::{Market, World};
pub use replay::{replay, Command, Event};
```

Comparison notes:

- Keep implementation modules private by default.
- Export only the API needed by tests or callers.
- Do not split files before responsibilities are visible.

## 009_iterators_collections

Expected answer shape:

- use `Vec` when ordering matters,
- use maps only when lookup matters,
- sort keys before deterministic iteration if using unordered collections.

Worked answer:

```rust
fn prices_in_market_order(world: &World) -> Vec<i32> {
    world.markets.iter().map(|market| market.price).collect()
}
```

Comparison notes:

- A plain loop would be equally acceptable.
- Readability wins over clever iterator chains.

## 010_state_hashing

Expected answer shape:

- hash canonical state,
- avoid unordered iteration,
- exclude nondeterministic fields.

Worked answer:

```rust
fn canonical_state(world: &World) -> String {
    let mut out = format!("tick:{}\n", world.tick);

    for (index, market) in world.markets.iter().enumerate() {
        out.push_str(&format!(
            "market:{index}:supply:{}:demand:{}:price:{}\n",
            market.supply, market.demand, market.price
        ));
    }

    out
}

#[test]
fn canonical_state_is_stable() {
    let world = World {
        tick: 1,
        markets: vec![Market {
            supply: 2,
            demand: 3,
            price: 4,
        }],
    };

    assert_eq!(
        canonical_state(&world),
        "tick:1\nmarket:0:supply:2:demand:3:price:4\n"
    );
}
```

Comparison notes:

- A real hash can come later.
- Canonical text is easier to inspect while learning.

## 011_property_tests

Expected answer shape:

- test invariants, not implementation details.

Worked property:

```rust
proptest::proptest! {
    #[test]
    fn price_never_drops_below_one(supply in 0i32..100, demand in 0i32..100) {
        let mut world = World {
            tick: 0,
            markets: vec![Market {
                supply,
                demand,
                price: 1,
            }],
        };

        for _ in 0..10 {
            world.step();
            prop_assert!(world.markets[0].price >= 1);
        }
    }
}
```

Comparison notes:

- Generated inputs are constrained to valid domain values.
- The property states a business/simulation invariant.

## 012_snapshot_tests

Expected answer shape:

- snapshot stable command/event output,
- review changes deliberately.

Worked answer:

```rust
#[test]
fn event_log_snapshot_is_stable() {
    let initial = World {
        tick: 0,
        markets: vec![Market {
            supply: 10,
            demand: 10,
            price: 100,
        }],
    };

    let commands = vec![Command::Tick];
    let (_world, events) = replay(initial, &commands);

    insta::assert_debug_snapshot!(events);
}
```

Comparison notes:

- Snapshot event logs, not noisy internal state.
- Sort or canonicalize output first if needed.

## 013_data_layout_probe

Expected answer shape:

- compare behavior-equivalent versions,
- do not optimize until both pass the same tests.

Acceptable conclusion:

```text
Array-of-structs is clearer for current exercises.
Struct-of-arrays may help later if market update profiling shows cache pressure.
Stay with array-of-structs for now.
```

## 014_concurrency_parallel_markets

Expected answer shape:

- parallelize independent market updates,
- collect results in stable order,
- compare against sequential implementation.

Worked answer outline:

```rust
fn step_market(market: &mut Market) {
    let pressure = market.demand - market.supply;
    market.price = (market.price + pressure.signum()).max(1);
}

fn step_sequential(markets: &mut [Market]) {
    for market in markets {
        step_market(market);
    }
}

fn step_parallel(markets: &mut [Market]) {
    use rayon::prelude::*;
    markets.par_iter_mut().for_each(step_market);
}
```

Comparison notes:

- This is safe because each market update is independent.
- Any cross-market effects need a deterministic reduction phase.

## 015_shared_ownership

Expected answer shape:

- compare IDs against `Rc<RefCell<T>>` or `Arc<Mutex<T>>`,
- prefer IDs for simulation world relationships unless a real shared ownership
  need appears.

Good conclusion:

```text
Stable IDs keep ownership centralized in World and make replay simpler.
Rc<RefCell<T>> makes mutation easier locally but hides aliasing and complicates
reasoning. Use IDs for core world state.
```

## 016_message_boundary

Expected answer shape:

- one owner mutates world state,
- commands cross the boundary,
- tests can run synchronously.

Worked answer outline:

```rust
struct Sim {
    world: World,
}

impl Sim {
    fn handle(&mut self, command: Command) -> Vec<Event> {
        apply(&mut self.world, &command)
    }
}
```

Comparison notes:

- Add channels only after this synchronous boundary is clear.
- The architectural point is single-writer ownership.

## 017_async_io_edge

Expected answer shape:

- async code receives or persists data,
- core simulation remains synchronous.

Good boundary:

```text
async input -> Command -> synchronous Sim::handle -> Event -> async output
```

Comparison notes:

- Do not make `World::step` async.
- Do not let IO timing affect simulation rules.

## 018_no_ecs_baseline

Expected answer shape:

- direct `World` data model,
- plain functions or methods as systems,
- tests define expected behavior.

Good conclusion:

```text
The direct model is clear enough for goods, markets, and simple agents.
Do not introduce ECS until agent/system interactions become hard to organize.
```

## 019_minimal_ecs

Expected answer shape:

- entities are IDs,
- components are maps or vectors,
- systems are explicit functions,
- ordering is controlled.

Good conclusion:

```text
Minimal ECS clarifies some component grouping but adds bookkeeping.
The benefit is not yet obvious for the current market model.
```

## 020_bevy_ecs_probe

Expected answer shape:

- reproduce the same behavior using `bevy_ecs`,
- compare schedule clarity, query ergonomics, and deterministic ordering.

Good conclusion format:

```text
Keep / Defer / Reject bevy_ecs for the core.

Reason:
- Clarity:
- Determinism:
- Testability:
- Friction:
```

## 03x_ecs_experiment

Expected answer shape:

- one question per experiment,
- same behavior as baseline,
- explicit conclusion.

Stop if:

- the experiment becomes framework design,
- behavior differs from baseline,
- determinism cannot be explained.

## 04x_godot_bridge

Expected answer shape:

- Rust produces state snapshots,
- Godot displays them,
- Godot sends commands,
- replay stays independent of Godot.

Good boundary:

```text
Rust core -> Snapshot DTO -> Godot view
Godot input -> Command DTO -> Rust core
```

Stop if:

- rules move into Godot,
- UI needs start reshaping core simulation state prematurely.

## 05x_async_io

Expected answer shape:

- async edge wraps the synchronous core,
- command ordering remains explicit,
- deterministic tests do not require Tokio.

Good boundary:

```text
Tokio task receives IO
Tokio task sends Command
Sim owns World
Sim emits Event
Tokio task writes response
```

Stop if:

- async spreads into pure simulation logic,
- runtime behavior changes replay results.

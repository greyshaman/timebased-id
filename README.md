# TimeBasedId Generator

A lightweight Rust library for generating unique identifiers based on system uptime and Unix timestamp. Perfect for applications that need simple, fast, and unique ID generation without external dependencies.

## Features

- 🚀 **Fast generation** - No network calls or complex computations
- 🔢 **128-bit identifiers** - Ample space for uniqueness
- 🎯 **Time-based** - Combines OS uptime and Unix timestamp
- 🧪 **No dependencies** - Minimal footprint (except for system uptime)
- 📦 **Simple API** - Easy to integrate and use

## How It Works

The generator creates a 128-bit ID by combining two components:

1. OS Uptime (shifted left by 64 bits)
2. Current Unix timestamp in nanoseconds

Formula: `ID = (uptime << 64) + current_unix_nanoseconds`

## Usage

Add this to your Cargo.toml:

```toml
[dependencies]

timebased-id = "0.1"
```

Basic usage:

```rust
use timebased_id::TimeBasedId;

fn main() {
    // Generate new Id:
    let id = TimeBasedId::default();

    // Get the numeric id
    let value = id.value();
    println!("Generated id: {}", value);

    // IDs are unique (for non-simultaneous generation )
    let id2 = TimeBasedId::default();
    assert_ne!(id.value(), id2.value());
}
```

## Ideal Use Cases

This generator is perfect when:
- Objects are created with time intervals greater than 1 nanosecond
- Systems reboot no more than once per second
- You need simple, fast, local ID generation
- You don't require strict chronological ordering across system reboots

## Project Structure

```text
src/
├── lib.rs          # Library exports
└── id.rs           # Core ID generation logic
```

## API Reference

`TimeBasedId`

The main struct representing a generated ID.

### Methods

- `default() -> Self` - Creates a new unique ID

- `value(&self) -> u128` - Returns the numeric value of the ID

### Traits Implemented

- `Debug`
- `Clone`
- `Eq`
- `PartialEq`
- `Hash`

## Development

Run test:

```bash
cargo test
```

## Performance

The generator is extremely fast as it only performs:

- One system call for uptime
- One system call for current time
- Two arithmetic operations

## License

MIT license in LICENSE file

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

# Alacritty - GPU-Accelerated Terminal Emulator

## Project Overview

Alacritty is a modern, fast, cross-platform, OpenGL terminal emulator written in Rust. It's designed to be a performant terminal emulator that comes with sensible defaults but allows for extensive configuration. The software is considered to be at a beta level of readiness, with active development ongoing.

### Architecture
The project is organized as a Rust workspace with multiple crates:
- `alacritty`: Main application crate (UI, event handling, window management)
- `alacritty_terminal`: Core terminal emulator library (PTY, grid, parsing)
- `alacritty_config`: Configuration system
- `alacritty_config_derive`: Configuration derive macros

### Key Technologies
- **Rust**: Primary programming language
- **OpenGL**: Graphics rendering backend
- **winit**: Window management and event handling
- **glutin**: OpenGL context creation
- **vte**: VT100/VT220/ECMA-48 terminal emulation
- **Cross-platform**: Support for BSD, Linux, macOS, and Windows

## Building and Running

### Prerequisites
- Rust 1.85.0+ (minimum supported Rust version)
- OpenGL ES 2.0+ capable graphics hardware
- Platform-specific requirements (e.g., X11/Wayland on Linux, ConPTY on Windows)

### Build Commands
```bash
# Build release binary (uses Cargo.toml workspace setup)
cargo build --release

# Build with specific features (default features: x11, wayland)
cargo build --features x11,wayland

# Build for specific target
cargo build --target x86_64-apple-darwin --release
```

### Using Makefile (macOS/Linux)
```bash
# Build native binary
make binary

# Build universal binary (macOS)
make binary-universal

# Create macOS app bundle
make app

# Create macOS DMG installer
make dmg
```

### Development Commands
```bash
# Run in development mode
cargo run

# Run with verbose logging
cargo run -- -vvv

# Run with reference test mode (for testing)
cargo run -- --ref-test

# Run tests
cargo test

# Format code (enforced by CI)
cargo fmt

# Check for linting issues
cargo clippy
```

## Project Structure
```
alacritty/                    # Main application (UI, event handling)
├── src/
│   ├── config/              # Configuration handling
│   ├── display/             # Display rendering logic
│   ├── input/               # Input processing
│   ├── renderer/            # OpenGL rendering
│   └── main.rs              # Application entry point
├── res/                     # Resource files
└── Cargo.toml               # Main application manifest

alacritty_terminal/          # Terminal emulator library
├── src/
│   ├── grid/                # Terminal grid implementation
│   ├── term/                # Terminal state machine
│   ├── tty/                 # Pseudo-terminal operations
│   └── lib.rs               # Public API exports
└── Cargo.toml               # Library manifest

alacritty_config/            # Configuration system
├── src/
└── Cargo.toml               # Config crate manifest

alacritty_config_derive/     # Derive macros for config
├── src/
└── Cargo.toml               # Config derive crate manifest
```

## Development Conventions

### Coding Standards
- All code must be formatted with `rustfmt` (enforced by CI)
- Comments must be fully punctuated with trailing periods
- Follow Rust API guidelines (https://rust-lang.github.io/api-guidelines)
- Use Unix-style line endings (`\n`)
- Wrap long comments (100 chars max)

### Testing
- All changes must pass `cargo test`
- Performance changes should be benchmarked with `vtebench`
- New functionality should include appropriate tests
- Reference tests are available for visual comparison

### Documentation
- Code should be documented where appropriate
- Configuration changes must be documented in man pages
- Changelog entries required for user-impacting changes
- Follow existing documentation patterns in the codebase

### Configuration System
- Config files use TOML format
- Multiple config file locations are searched (XDG Base Dir Spec compliant)
- Configuration monitoring is live-updating during runtime

## Platform Support
- **Linux/BSD**: X11 and Wayland support with copypasta integration
- **macOS**: Full Retina display support, system integration
- **Windows**: ConPTY backend support (Windows 10 version 1809+)

## Key Features
- GPU-accelerated rendering via OpenGL
- Cross-platform with consistent behavior
- Performant terminal emulation using the vte parser
- Extensive configuration options
- Live configuration reloading
- Clipboard integration
- Mouse support
- Unicode support

## Entry Points
- **Main application**: `alacritty/src/main.rs` - Initializes window, config, event loop, and PTY
- **Terminal core**: `alacritty_terminal/src/lib.rs` - Exports Grid and Term structures
- **Configuration**: `alacritty_config/src/lib.rs` - Configuration loading and validation

## Common Development Tasks
```bash
# Update dependencies
cargo update

# Check all workspace crates
cargo check --workspace

# Run specific test
cargo test test_name

# Build documentation
cargo doc --workspace --open

# Create new release version
# Follow release process in CONTRIBUTING.md
```

## Important Files
- `Cargo.toml` - Workspace configuration and crate dependencies
- `README.md` - Project overview and installation
- `CONTRIBUTING.md` - Contribution guidelines
- `Makefile` - Build automation scripts
- `rustfmt.toml` - Formatting configuration
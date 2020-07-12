# cliptard

Cliptard is a cross-platform library for getting and setting the contents of the OS-level clipboard.  It is a fork of [rust-clipboard](https://github.com/aweinstock314/rust-clipboard).

It has been tested on Windows, Mac OSX, GNU/Linux, and FreeBSD.

## Prerequisites

On Linux you need the x11 library, install it with something like:

```bash
sudo apt-get install xorg-dev
```

## Example

```rust
use cliptard::{ClipboardProvider, ClipboardContext};

fn main() {
    let mut context: ClipboardContext = ClipboardProvider::new().unwrap();
    println!("{:?}", context.get_contents());
    context.set_contents("some string".to_owned()).unwrap();
}
```

## API

The `ClipboardProvider` trait has the following functions:

```rust
fn new() -> Result<Self, Box<Error>>;
fn get_contents(&mut self) -> Result<String, Box<Error>>;
fn set_contents(&mut self, String) -> Result<(), Box<Error>>;
```

`ClipboardContext` is a type alias for one of {`WindowsClipboardContext`, `OSXClipboardContext`, `X11ClipboardContext`, `NopClipboardContext`}, all of which implement `ClipboardProvider`. Which concrete type is chosen for `ClipboardContext` depends on the OS (via conditional compilation).

# License

This project is licensed under either of

 * Apache License, Version 2.0, ([LICENSE-APACHE](LICENSE.apache2) or
   http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE.mit](LICENSE-MIT) or
   http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion by you, as defined in the Apache-2.0 license, shall be dual
licensed as above, without any additional terms or conditions.

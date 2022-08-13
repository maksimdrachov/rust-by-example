Printing is handled by a series of `macros` defined in `std::fmt` some of which include:

- `format!`: write formatted text to `String`
- `print!`: same as `format!` but the text is printed to the console (io::stdout)
- `println!`: same as `print!` but a newline is appended
- `eprint!`: same as `format!` but the text is printed to the standard error (io::stderr)
- `eprintln!`: same as `eprint!` byt a newline is appended

In general `{}` will be automatically replaced with any arguments. These will be stringified.

Only types that implement `fmt::Display` can be formatted with `{}`. User-defined types do not implement `fmt::Display` by default.

`std::fmt` (fmt means format) contains many `traits` which govern the display of text. The base form of two important ones are listed below:
- `fmt::Debug`: Uses the `{:?}` marker. Format text for debugging purposes.
- `fmt::Display`: Uses the `{}` marker. Format text in a more elegant, user-friendly fashion.

## Debug

```rust
// The derive attribute automatically creates the implementation
// required to make this struct printable with fmt::Debug
struct DebugPrintable(i32);
```
## Display

Manually implementing `fmt::Display`, which uses the `{}` print marker. Implementing this:

```rust
// Import the fmt module to make it available
use std::fmt;

// Define a structure for which fmt::Display will be implemented. 
// This is a tuple struct named Structure that contains an i32
struct Structure(i32);

// To use the {} marker, the trait fmt::Display must be implemented manually
impl fmt::Display for Structure {
    // This trait requires fmt with this exact signature
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Write strictly the first element into the supplied output
        // stream: f. Returns fmt::Result which indicates whether the operation succeeded or failed. 
        // Note that write! uses syntax which is very similar to println!
        write!(f, "{}", self.0)
    }
}
```
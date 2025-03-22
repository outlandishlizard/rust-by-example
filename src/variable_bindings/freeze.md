# Shadowing and mutability

When shadowing mutable data, it is possible to make the shadowed variable immutable. This can be useful for temporarily making a mutable immutable within a scope.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // Just assigning to an immutable from it will not cause _mutable_integer 
        // to become immutable.
        let x = _mutable_integer;
        _mutable_integer = 123;
        println!("x was assigned the value of _mutable_integer: {}",x);

        // But shadowing it with an immutable will:
        let _mutable_integer = _mutable_integer;
        // FIXME ^ Comment out this line
        // Error! `_mutable_integer` is immutable in this scope
        _mutable_integer = 50;
        
        // The shadowing `_mutable_integer` goes out of scope
    }

    // Ok! `_mutable_integer` is mutable again!
    println!("The value change from inside the scope persists: {}", _mutable_integer);
    _mutable_integer = 3;
    println!("And _mutable_integer is mutable again: {}", _mutable_integer);
}
```
It is less clearly useful, but the opposite is also possible-- you can shadow an immutable with a mutable.

```rust,editable,ignore,mdbook-runnable
    let _immutable_integer = 0;
    {
        let mut _immutable_integer = _immutable_integer;
        _immutable_integer = 1;
        println!("Shadowed an immutable with a mutable: {}",_immutable_integer);
        // The shadowing `_immutable_integer` goes out of scope
    }
    _immutable_integer = 2;
    // FIXME ^ Comment out this line.
    println!("Changes from the mutable inside the scope do not persist outside: {}", _immutable_integer)
  
```

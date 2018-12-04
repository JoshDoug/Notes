# Rust Unit Testing

Rust has basic unit test support baked in with Cargo. A function can be annotated with an 'attribute': `#[test]` which ensures the function is ignored during normal compilation and builds.
These unit tests can be run with cargo: `cargo test`.

Example of a single file program with a function that finds the greatest common denominator (gcd) and includes a unit test for it:

```rust
fn main() {
    println!("{}", gcd(30, 35));
}

fn gcd(mut n: u64, mut m: u64) -> u64 {
    assert!(n != 0 && m != 0);
    while m != 0 {
        if m < n {
            let t = m;
            m = n;
            n = t;
        }
        m = m % n;
    }
    n
}

#[test]
fn test_gcd() {
    assert_eq!(gcd(14,15), 1);

    assert_eq!(gcd(2 * 3 * 5 * 11 * 17, 3 * 7 * 11 * 13 * 19), 3 * 11);
}
```

Of course unit tests don't have to be in the same file...need to check that out though, TKTK.
[![Build Status](https://travis-ci.org/durch/rust-jwt.svg?branch=master)](https://travis-ci.org/durch/rust-jwt)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/durch/rust-jwt/blob/master/LICENSE)
[![](http://meritbadge.herokuapp.com/smpl-jwt)](https://crates.io/crates/smpl-jwt)
[![Join the chat at https://gitter.im/durch/rust-jwt](https://badges.gitter.im/durch/rust-jwt.svg)](https://gitter.im/durch/rust-jwt?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## rust-jwt [[docs](https://docs.rs/smpl-jwt)]

Very simple [JWT](https://jwt.io/) generation lib, provides a JWT struct which can be *finalised* to produce an encoded and signed [String](https://doc.rust-lang.org/std/string/struct.String.html) representation.

Generic over [serde::ser::Serialize](https://docs.serde.rs/serde/ser/trait.Serialize.html) trait.

### Usage

Jwt can be finalized to produce an encoded and signed string representation.

```rust
use serde::Serialize;
use smpl_jwt::{Jwt, RSAKey};

#[derive(Serialize)]
struct ExampleStruct {
    field: String,
}

fn main() {
    let rsa_key = match RSAKey::from_pem("random_rsa_for_testing") {
        Ok(x) => x,
        Err(e) => panic!("{}", e),
    };

    let jwt = Jwt::new(
        ExampleStruct {
            field: String::from("test"),
        },
        rsa_key,
        None,
    );

    println!("{}", jwt);
}
```

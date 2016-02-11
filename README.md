# afterparty

[![Build Status](https://travis-ci.org/softprops/afterparty.svg?branch=master)](https://travis-ci.org/softprops/afterparty)

> what happens on github...

## docs

Find them [here](http://softprops.github.io/afterparty)

# usage

Afterparty has to key abstractions a `Hook`, a handler of webhook deliveries, and a `Hub`, a registry for hooks. A `Hub` delivers `Deliveries` to interested hooks.

A `Delivery` encodes all relevant webhook request information including a unique identifier for the delivery, the event name, and typed payload of represented as an enumerated type of `Event`.

Hubs implements hyper's Server Handler trait so that it may be mounted into any hyper Server.

```rust
extern crate afterparty;
extern create hyper;

use hyper::Server;
use afterparty::{Delivery, Hub};

fn main() {
    let mut hub = Hub::new();
    hub.handle("*", |delivery: &Delivery| {
        println!("rec delivery {:#?}", delivery)
    });
    hub.handle_authenticated("push", "secret", |delivery: &Delivery| {
       println!("rec authenticated delivery {:#?}", delivery)
    });
    let svc = Server::http("0.0.0.0:4567")
       .handle(hub)
    println!("hub is up");
    srv.unwrap();
}
```

## building

* build a release binary

```bash
$ docker run -it --rm -v $(pwd):/source jimmycuadra/rust:1.2.0
cargo build --release
exit
```

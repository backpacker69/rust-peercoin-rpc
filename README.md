# Rust RPC client for Peercoin JSON-RPC

This is a Rust RPC client library for calling the Peercoin JSON-RPC API. It provides a layer of abstraction over
[rust-jsonrpc](https://github.com/apoelstra/rust-jsonrpc) and makes it easier to talk to the Peercoin JSON-RPC interface

This git package compiles into two crates.
1. [peercoin-rpc](https://crates.io/crates/peercoin-rpc) - contains an implementation of an rpc client that exposes
the Peercoin JSON-RPC APIs as rust functions.

2. [peercoin-rpc-json](https://crates.io/crates/peercoin-rpc-json) -  contains rust data structures that represent
the json responses from the Peercoin JSON-RPC APIs. peercoin-rpc depends on this.

# Usage
Given below is an example of how to connect to the Peercoin JSON-RPC for a Peercoin node running on `localhost`
and print out the hash of the latest block.

It assumes that the node has password authentication setup, the RPC interface is enabled at port `8332` and the node
is set up to accept RPC connections.

```rust
extern crate peercoin_rpc;

use peercoin_rpc::{Auth, Client, RpcApi};

fn main() {

    let rpc = Client::new("http://localhost:9902",
                          Auth::UserPass("<FILL RPC USERNAME>".to_string(),
                                         "<FILL RPC PASSWORD>".to_string())).unwrap();
    let best_block_hash = rpc.get_best_block_hash().unwrap();
    println!("best block hash: {}", best_block_hash);
}
```

See `client/examples/` for more usage examples.

# Supported Bitcoin Core Versions
The following versions are officially supported and automatically tested:
* 0.12.7
* 0.13.0

# Minimum Supported Rust Version (MSRV)
This library should always compile with any combination of features on **Rust 1.41.1**.

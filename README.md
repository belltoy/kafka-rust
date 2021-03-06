# Kafka Rust Client

[![Build Status](https://travis-ci.org/spicavigo/kafka-rust.svg?branch=master)](https://travis-ci.org/spicavigo/kafka-rust) [![](http://meritbadge.herokuapp.com/kafka)](https://crates.io/crates/kafka)

### Documentation

* This library is primarily documented through examples in its API
documentation:
  * [0.6](https://docs.rs/kafka/^0.6)
  * [0.5](https://docs.rs/kafka/^0.5)
* Documentation about Kafka itself can be found at [its project
home page](http://kafka.apache.org/).


### Installation

This crate works with Cargo and is on
[crates.io](https://crates.io/crates/kafka).  The API is currently
under heavy movement although we do follow semantic versioning (but
expect the version number to grow quickly.)

```toml
[dependencies]
kafka = "0.6"
```

To build kafka-rust the usual `cargo build` should suffice.  The crate
supports various features which can be turned off at compile time.
See kafka-rust's `Cargo.toml` and [cargo's
documentation](http://doc.crates.io/manifest.html#the-features-section).

### Supported Kafka version

`kafka-rust` is tested against Kafka 0.8.2.x and regularly used
against Kafka 0.9 servers.  However, efforts to implement support for
new features from the Kafka 0.9 release are just in their beginnings.


### Examples

As mentioned, the [cargo generated
documentation](https://docs.rs/kafka/) constains some examples.
Further, standalone, compilable example programs are provided in the
[examples directory of the
repository](https://github.com/spicavigo/kafka-rust/tree/master/examples).


### Consumer

This is a higher-level consumer API for Kafka and is provided by the
module `kafka::consumer`.  It provides convenient offset management
support on behalf of a specified group.  This is the API a client
application of this library wants to use for receiving messages from
Kafka.


### Producer

This is a higher-level producer API for Kafka and is provided by the
module `kafka::producer`.  It provides convenient automatic partition
assignment capabilities through partitioners.  This is the API a
client application of this library wants to use for sending messsages
to Kafka.


### KafkaClient

`KafkaClient` in the `kafka::client` module is the central point of
this API.  However, this is a mid-level abstraction for Kafka rather
suitable for building higher-level APIs.  Application's typically want
to use the already mentioned `Consumer`s and `Producer`s.
Nevertheless, `KafkaClient`'s main features are:

* Loading metadata
* Fetching topic offsets
* Sending messages
* Fetching messages
* Committing a consumer group's offsets
* Fetching a consumer group's offsets


### Bugs / Features / Contributing

There's still a lot of potential for improvements on `kafka-rust`.
Not everything works right at the moment.  Have a look into the [issue
tracker](https://github.com/spicavigo/kafka-rust/issues) and feel free
to contribute by reporting new problems or contributing to existing
ones.  Any constructive feedback is warmly welcome!

As usually with open source, don't hesitate to fork the repo and
submit a pull requests if you see something to be changed.  We'll be
happy see `kafka-rust` improving over time.

### Integration tests

When working locally, the integration tests require that you must have
Docker (1.10.0+) and docker-compose (1.6.0+) installed and run the tests via the
included `run-all-tests` script in the `tests` directory. See the `run-all-tests`
script itself for details on its usage.


### Creating a topic

Note unless otherwise explicitely stated in the documentation, this
library will ignore requests to topics which it doesn't know about.
In particular it will not try to retrieve messages from
non-existing/unknown topics.  (This behavior is very likely to change
in future version of this library.)

Given a local kafka server installation you can create topics if the
following command (`kafka-topics.sh` is part of the Kafka
distribution):

```
kafka-topics.sh --topic my-topic --create --zookeeper localhost:2181  --partition 1 --replication-factor 1
```

See also [Kafka's quickstart guide](https://kafka.apache.org/documentation.html#quickstart)
for more information.


### Alternative/Related projects

* [rust-rdkafka](https://github.com/fede1024/rust-rdkafka) is an
  emerging alternative Kafka client library for Rust based on
  `librdkafka`.

# rust-lambda-builder

This is a quick thing I put together for local building of Lambda functions built using Rust. This is heavily based on the official Docker Hub [Rust Image](https://hub.docker.com/_/rust) but replaces the Distribution with Amazon Linux. This allows for your Lambda functions to be compiled agains the right runtime without the need for a full EC2 instance to do so.

## Building

```bash
docker build . -t rust-lambda-builder
```

## Building your lambda

Run something along the lines of:

```bash
docker run --rm \
           --user "$(id -u)":"$(id -g)" \
           -v "$PWD":/usr/src/myapp \
           -w /usr/src/myapp \
           rust-lambda-builder \
           cargo build --release
```

It'll put the output in target/release and you can package up the usual way.

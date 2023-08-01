FROM debian:buster-slim

ENV RUSTUP_ARCH=x86_64-unknown-linux-gnu
ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

RUN apt-get update \
    && apt-get install -y --no-install-recommends ca-certificates gcc libc6-dev wget \
    && wget "https://static.rust-lang.org/rustup/dist/$RUSTUP_ARCH/rustup-init" \
    && chmod +x /rustup-init \
    && ./rustup-init -y --no-modify-path --default-toolchain nightly --default-host=$RUSTUP_ARCH \
    && rm rustup-init \
    && chmod -R a+w $RUSTUP_HOME $CARGO_HOME \
    && rustup --version \
    && cargo --version \
    && rustc --version \
    && apt-get remove -y --auto-remove wget \
    && rm -rf /var/lib/apt/lists/*

RUN cargo install cargo-chef --locked
RUN apt update && apt-get install -y musl-tools
RUN rustup target add x86_64-unknown-linux-musl

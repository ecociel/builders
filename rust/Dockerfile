FROM debian:buster-slim

ARG BUILDPLATFORM
ARG TARGETPLATFORM
ARG TARGETOS
ARG TARGETARCH

RUN echo "AAAA "$BUILDPLATFORM
RUN echo "BBBB "$TARGETPLATFORM
RUN echo "CCCC "$TARGETARCH
RUN echo "DDDD "$TARGETOS

RUSTUP_ARCH=x86_64-unknown-linux-musl
ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

# "amd64")  RUSTUP_ARCH=x86_64-unknown-linux-gnu ;; \
# "arm64")  RUSTUP_ARCH=aarch64-unknown-linux-gnu ;; \

#RUN apt-get update \
#    && apt-get install -y --no-install-recommends ca-certificates gcc libc6-dev wget \
#    &&  case ${TARGETARCH} in \
#                "amd64")  RUSTUP_ARCH=x86_64-unknown-linux-musl ;; \
#                "arm64")  RUSTUP_ARCH=aarch64-unknown-linux-musl ;; \
#            esac \
#    && wget "https://static.rust-lang.org/rustup/dist/$RUSTUP_ARCH/rustup-init" \
#    && chmod +x /rustup-init \
#    && ./rustup-init -y --no-modify-path --default-toolchain nightly --default-host=$RUSTUP_ARCH \
#    && rm rustup-init \
#    && chmod -R a+w $RUSTUP_HOME $CARGO_HOME \
#    && rustup --version \
#    && cargo --version \
#    && rustc --version \
#    && apt-get remove -y --auto-remove wget \
#    && rm -rf /var/lib/apt/lists/*


RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates gcc libc6-dev wget
  && wget "https://static.rust-lang.org/rustup/dist/${RUSTUP_ARCH}/rustup-init" \
  && chmod +x /rustup-init \
  && ./rustup-init -y --no-modify-path --default-toolchain nightly --default-host=${RUSTUP_ARCH} \
  && rm rustup-init \
  && chmod -R a+w $RUSTUP_HOME $CARGO_HOME \
  && rustup --version \
  && cargo --version \
  && rustc --version \
  && apt-get remove -y --auto-remove wget \
  && rm -rf /var/lib/apt/lists/* \
  && apt update && apt-get install -y musl-tools \
  && rustup target add ${RUSTUP_ARCH} \

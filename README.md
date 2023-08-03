# rust-builder

A builder image for building static rust binaries for multiple platforms.

# Usage

~~~~
FROM ghcr.io/ecociel/rust-builder:1.73.0-nightly as builder

ARG TARGETARCH

RUN useradd -u 10001 scratchuser
WORKDIR /usr/local/src/app
COPY . .
RUN case ${TARGETARCH} in \
                "amd64")  MUSL_ARCH=x86_64-unknown-linux-musl ;; \
                "arm64")  MUSL_ARCH=aarch64-unknown-linux-musl ;; \
            esac \
   && cargo build --release --target ${MUSL_ARCH} --package myapp \
   && mv /usr/local/src/app/target/${MUSL_ARCH}/release/myapp /usr/local/bin/app

FROM scratch AS runtime
COPY --from=builder /usr/local/bin/app /app
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=builder /etc/passwd /etc/passwd

USER scratchuser

CMD ["/app"]

~~~~

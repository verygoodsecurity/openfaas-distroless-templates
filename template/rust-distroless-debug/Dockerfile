FROM openfaas/classic-watchdog:0.18.0 as watchdog

# Build Stage
FROM rust:1.37.0-alpine AS builder

RUN rustup target add x86_64-unknown-linux-musl

RUN USER=root
WORKDIR /usr/src/openfaas
COPY function ./function
COPY main ./main

RUN cd main && cargo build --release
RUN cd main && cargo install --target x86_64-unknown-linux-musl --path .

# Runner stage
FROM gcr.io/distroless/cc:debug
WORKDIR /home/nobody
USER nobody

COPY --from=watchdog /fwatchdog .
COPY --from=builder /usr/local/cargo/bin/main .

ENV fprocess="./main"

HEALTHCHECK --interval=5s CMD [ -e /tmp/.lock ] || exit 1

CMD ["./fwatchdog"]


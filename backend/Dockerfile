FROM rust:1.65.0-alpine3.16 AS builder
RUN apk upgrade --update-cache --available && \
    apk add build-base
COPY ./backend ./app/backend
COPY ./database ./app/database
COPY ./shared ./app/shared
RUN cargo build --release --manifest-path /app/backend/Cargo.toml

FROM alpine:3.16
COPY --from=builder /app/backend/target/release /target/release/backend
RUN ["chmod", "+x", "/target/release/backend"]
EXPOSE 8080
CMD ["/target/release/backend/backend"]
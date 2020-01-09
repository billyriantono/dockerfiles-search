# docker build --rm -t my_blog .
FROM rust:1.36-stretch as builder

# Step 1: download dependencies

# # Note: This is registry for Chinese User
# RUN echo '[source.crates-io]' > /usr/local/cargo/config && \
#     echo 'registry = "https://github.com/rust-lang/crates.io-index"' >> /usr/local/cargo/config && \
#     echo 'replace-with = "ustc"' >> /usr/local/cargo/config && \
#     echo '[source.ustc]' >> /usr/local/cargo/config && \
#     echo 'registry = "https://mirrors.ustc.edu.cn/crates.io-index"' >> /usr/local/cargo/config 
WORKDIR /app
RUN USER=root cargo init
COPY ./Cargo.toml ./
RUN echo 'fn main() { println!("Good") }' > ./src/main.rs
RUN cargo build --release

# Step 2: build application

RUN rm -r target/release/.fingerprint/my_blog-*
COPY . .
RUN cargo build --release

# Step 3: Copy app to ubuntu image

FROM ubuntu:latest

# Note: This is to prepare for sqlite
RUN apt-get update && apt-get -y install sqlite3 
RUN apt-get -y install vim curl
WORKDIR /app
COPY --from=builder /app/target/release/client /app/client
COPY --from=builder /app/target/release/server /app/server
COPY ./static /app/static

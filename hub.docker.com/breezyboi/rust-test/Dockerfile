# select image
FROM rust:1.36

# copy the curreny directory contents into the container
COPY ./ ./

# build for release
RUN cargo build --release

# set the startup command to run the binary
CMD ["./target/release/myproject"]
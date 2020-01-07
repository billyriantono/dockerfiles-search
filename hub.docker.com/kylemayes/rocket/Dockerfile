FROM kylemayes/rust

# Compile Rocket
ADD . app
RUN cd app && cargo build --release && rm Cargo.lock Cargo.toml lib.rs

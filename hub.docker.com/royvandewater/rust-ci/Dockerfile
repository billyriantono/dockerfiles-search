FROM circleci/rust:latest

RUN cargo install cargo2junit

CMD cargo test -- -Z unstable-options --format json | cargo2junit > results.xml


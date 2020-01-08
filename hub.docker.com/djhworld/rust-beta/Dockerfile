FROM debian:wheezy

RUN apt-get update -y && apt-get install -y --no-install-recommends wget gcc libc-dev
RUN mkdir /rust && wget -q --no-check-certificate  https://static.rust-lang.org/dist/rust-1.0.0-beta-x86_64-unknown-linux-gnu.tar.gz -O - | tar xzf - -C /rust --strip-components=1 && /rust/install.sh && rm -rf /rust

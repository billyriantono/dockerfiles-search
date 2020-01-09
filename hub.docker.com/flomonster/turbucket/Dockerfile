FROM rust:latest as build

RUN rustup update nightly && rustup default nightly
RUN cargo  install --git https://github.com/flomonster/turbucket.git --root /tmp

FROM rust:latest

COPY --from=build /tmp/bin/turbucket turbucket

ENV ROCKET_ADDRESS 0.0.0.0
ENV ROCKET_PORT 80

EXPOSE 80

CMD ./turbucket

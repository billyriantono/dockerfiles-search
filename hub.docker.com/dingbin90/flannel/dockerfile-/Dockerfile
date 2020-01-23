FROM rust:1.19.0

WORKDIR /usr/src/myapp
COPY . .

ENV DATA_PATH=/tmp/data/data.zip

EXPOSE 80

RUN cargo install

CMD ["rust"]
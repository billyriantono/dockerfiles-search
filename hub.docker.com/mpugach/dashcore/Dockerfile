FROM debian:stable-slim

LABEL maintainer="Maksym Pugach <pugach.m@gmail.com>"

RUN mkdir -p /dash

WORKDIR /dash

RUN apt-get update -y \
 && apt-get install -y curl \
 && curl -OL https://github.com/dashpay/dash/releases/download/v0.12.3.2/dashcore-0.12.3.2-x86_64-linux-gnu.tar.gz \
 && echo '1c80bc79451da100c38c431fc8f9ff8e35e6f30a65df7b4200f8b01344453c70  dashcore-0.12.3.2-x86_64-linux-gnu.tar.gz' | sha256sum -c \
 && tar -xzvf dashcore-0.12.3.2-x86_64-linux-gnu.tar.gz -C . --strip-components=1 \
 && rm -rf share/ dashcore-0.12.3.2-x86_64-linux-gnu.tar.gz \
 && apt-get clean

ENV DASH_DATA="/home/dash/.dash" PATH="/dash/bin:$PATH"

COPY docker-entrypoint.sh /entrypoint.sh

RUN chmod u+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["dashd"]

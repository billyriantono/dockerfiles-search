FROM crystallang/crystal:0.26.1

RUN git clone https://github.com/cloudamqp/amqproxy /tmp/amqproxy && mkdir /tmp/amqproxy/bin

WORKDIR /tmp/amqproxy
RUN git checkout tags/v0.2.2
RUN crystal build --release -o bin/amqproxy src/amqproxy.cr
RUN cp bin/amqproxy /usr/bin/

CMD ["amqproxy"]

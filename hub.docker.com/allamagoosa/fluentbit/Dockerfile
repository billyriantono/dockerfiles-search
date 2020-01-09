FROM fluent/fluent-bit:0.13

COPY fluent-bit.conf /fluent-bit/etc/fluent-bit.conf
RUN apt-get update -y && apt-get -y install curl netcat

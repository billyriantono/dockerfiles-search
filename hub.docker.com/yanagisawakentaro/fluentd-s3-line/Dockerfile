FROM fluent/fluentd:v1.3.2

RUN ["gem", "install", "fluent-plugin-s3", "-v 1.1.8"]
RUN ["gem", "install", "fluent-plugin-line-notify"]
COPY fluent.conf /fluentd/etc/fluent.conf


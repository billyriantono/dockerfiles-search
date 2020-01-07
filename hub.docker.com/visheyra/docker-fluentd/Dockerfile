FROM fluent/fluentd:v1.2.5-debian

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install -y build-essential ruby-dev

RUN fluent-gem install fluent-plugin-rewrite-tag-filter fluent-plugin-nats fluent-plugin-elasticsearch fluent-plugin-prometheus fluent-plugin-kubernetes_metadata_filter fluent-plugin-systemd
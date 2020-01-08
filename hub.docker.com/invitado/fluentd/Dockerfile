FROM fluent/fluentd-kubernetes-daemonset:v1.3.3-debian-cloudwatch-1.4

# Install rewrite_tag_filter pluging.
RUN fluent-gem install fluent-plugin-rewrite-tag-filter

# Remove default configuration.
RUN rm -f /fluentd/etc/systemd.conf /fluentd/etc/prometheus.conf /fluentd/etc/kubernetes.conf /fluentd/etc/fluent.conf

# Add custom configuration.
COPY phpfpm.conf /fluentd/etc/phpfpm.conf
COPY public-webserver.conf /fluentd/etc/public-webserver.conf
COPY webserver.conf /fluentd/etc/webserver.conf
COPY fluent.conf /fluentd/etc/fluent.conf

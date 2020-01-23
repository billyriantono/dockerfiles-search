FROM fluent/fluentd-kubernetes-daemonset:v0.12.43-cloudwatch
COPY entrypoint.sh /bin/
ENTRYPOINT ["/bin/entrypoint.sh"]
CMD exec fluentd -c /fluentd/etc/${FLUENTD_CONF} -p /fluentd/plugins $FLUENTD_OPT

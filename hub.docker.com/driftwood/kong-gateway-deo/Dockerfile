FROM segment/chamber:2.7.5 as build

FROM kong:1.4.2

LABEL "com.datadoghq.ad.check_names"='["kong"]'
LABEL "com.datadoghq.ad.init_configs"='[{}]'
LABEL "com.datadoghq.ad.instances"='[{"kong_status_url": "http://kong.api:8100/status/"}]'


EXPOSE 8000 8001 8100

COPY --from=build /chamber /chamber
ENTRYPOINT ["/chamber", "exec", "kong", "datadog", "--", "/docker-entrypoint.sh"]

STOPSIGNAL SIGQUIT
CMD ["kong", "docker-start"]
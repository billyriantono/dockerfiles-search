FROM hairyhenderson/gomplate:v2.8.0 AS gomplate

FROM gocd/gocd-agent-debian-8:v18.9.0

COPY --from=gomplate /gomplate /usr/local/bin



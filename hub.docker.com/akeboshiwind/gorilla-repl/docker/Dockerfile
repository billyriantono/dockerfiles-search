FROM agrozyme/alpine:3.11
COPY rootfs /
RUN set +e -uxo pipefail && chmod +x /usr/local/bin/* && /usr/local/bin/docker-build.lua
CMD ["/usr/local/bin/docker-run.lua"]

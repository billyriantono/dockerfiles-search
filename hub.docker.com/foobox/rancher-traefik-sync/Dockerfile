FROM alpine:3.8

COPY src /
RUN rancher-traefik-sync-setup

ENTRYPOINT ["rancher-traefik-sync-entrypoint"]
CMD ["rancher-traefik-sync", "sync"]

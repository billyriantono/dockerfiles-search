FROM gitea/gitea:1
RUN apk --no-cache add libcap && \
    setcap cap_net_bind_service=+ep /app/gitea/gitea
CMD /usr/bin/entrypoint

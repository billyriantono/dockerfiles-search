FROM alpine:latest
COPY --from=nginx:alpine / /
COPY --from=linuxserver/qbittorrent / /
WORKDIR /
COPY entrypoint.sh ./
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY qBittorrent.conf /root/.config/qBittorrent/qBittorrent.conf
RUN apk add --no-cache openssh-client && chmod +x ./entrypoint.sh && mkdir downloads
ENTRYPOINT ["./entrypoint.sh"]
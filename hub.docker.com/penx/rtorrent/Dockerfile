FROM alpine:3.5
RUN apk add --update rtorrent
EXPOSE 6881 5000
COPY rtorrent.rc /root/.rtorrent.rc
CMD ["rtorrent"]

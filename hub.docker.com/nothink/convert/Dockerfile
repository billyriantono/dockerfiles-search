FROM alpine:3.8

# install pkgs
RUN apk add --update --no-cache imagemagick

# usage: waifu2x -i hoge.png -o moge.png
ENTRYPOINT ["convert"]
CMD ["--help"]

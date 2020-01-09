FROM node:alpine

RUN apk add --no-cache \
vim

WORKDIR /

COPY .vimrc /

ENTRYPOINT ["vim"]
CMD ["."]

EXPOSE 1337

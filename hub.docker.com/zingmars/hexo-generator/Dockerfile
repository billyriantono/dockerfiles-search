FROM alpine:latest
LABEL maintainer="Ingmars Melkis <contact@zingmars.me>"

RUN apk add npm git rsync
RUN npm install -g hexo

# Inside your CI config run npm update while inside your hexo directory.
# To avoid having to pull the whole thing over and over again just cache node_modules.
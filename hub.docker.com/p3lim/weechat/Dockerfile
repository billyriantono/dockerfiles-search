FROM p3lim/alpine:3.7

ENV LANG='C.UTF-8'

# install deps for plugins
RUN apk add --no-cache python2

# install weechat from edge, with plugin support
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main \
	weechat weechat-aspell weechat-lua weechat-perl weechat-ruby weechat-python

# add local files
COPY root/ /

# expose ourselves
EXPOSE 6667 6697 9000
VOLUME /config

# run weechat as an interactive process so we can attach to it
CMD ["/usr/bin/with-contenv", "s6-setuidgid", "abc", "/usr/bin/weechat", "-d", "/config/weechat"]

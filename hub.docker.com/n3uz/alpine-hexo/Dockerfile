FROM alpine
ENV TZ "Asia/Shanghai"
ENV PS1 "\[\033[0;32m\]\A \[\033[0;31m\]\u\[\033[0;34m\]@\[\033[0;35m\]\h\[\033[0;34m\]:\[\033[00;36m\]\w\[\033[0;33m\] -> \$ \[\033[0m\] "
RUN apk add --update \
    bash git nodejs nodejs-npm \
    && npm install hexo-cli -g \
	&& hexo init blog \
    && rm -rf /var/cache/apk/*
CMD /bin/bash
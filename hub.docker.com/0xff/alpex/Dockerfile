FROM alpine:3.2
RUN \
    apk add --update bash git curl tig && \
    rm -rf /var/cache/apk/* && \
    git config --global user.name docker-alpex && \
    git config --global user.email docker-alpex@bytecast.net && \
    echo 'PS1="\u@\h \w\n# "' >> /root/.profile && \
    echo 'alias l="ls --color=auto -lah"' >> /root/.profile

CMD bash -l

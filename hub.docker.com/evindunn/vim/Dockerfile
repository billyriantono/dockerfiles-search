FROM alpine:latest

RUN apk add --update --no-cache     \
        bash                        \
        tini                        \
        vim                         \
    && rm -rf /var/cache/apk/*

SHELL ["/bin/bash", "-c"]

ADD vimrc /etc/vim/
ADD alias.sh /etc/profile.d/

RUN chmod +x /etc/profile.d/alias.sh

ENTRYPOINT ["tini", "--"]
CMD ["/bin/bash", "--login"]

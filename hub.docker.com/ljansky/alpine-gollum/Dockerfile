FROM alpine:3.7

RUN apk update && \
    apk add ruby ruby-dev ruby-rake ruby-rdoc cmake bash openssh-client \
        libffi-dev build-base git zlib-dev icu-dev && \
    gem install --no-ri --no-rdoc gollum github-markdown redcarpet && \
    apk del build-base ruby-dev && \
    rm -rf /root/src /tmp/* /usr/share/man /var/cache/apk/*

RUN mkdir /root/wikidata
RUN git init /root/wikidata

# Expose default gollum port 4567
EXPOSE 4567

WORKDIR /root/wikidata

ADD ./init_wiki.sh /root/
RUN chmod 777 /root/init_wiki.sh

ADD ./post-commit.sh /root/wikidata/.git/hooks/post-commit
RUN chmod a+x /root/wikidata/.git/hooks/post-commit

ADD ./config.rb /root/config.rb

ENTRYPOINT /root/init_wiki.sh "$SUB_MODULE_NAME"
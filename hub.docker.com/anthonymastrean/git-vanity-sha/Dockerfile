FROM ruby:alpine

LABEL maintainer "Anthony Mastrean <anthony.mastrean@gmail.com>"

RUN apk --no-cache --update add \
        git \
        git-lfs \
        openssh \
    && wget -q -O /usr/local/bin/git-vanity-sha https://raw.githubusercontent.com/AnthonyMastrean/git-vanity-sha/patch-1/git-vanity-sha \
    && chmod +x /usr/local/bin/git-vanity-sha

VOLUME ["/git"]

WORKDIR /git

ENTRYPOINT ["git-vanity-sha"]

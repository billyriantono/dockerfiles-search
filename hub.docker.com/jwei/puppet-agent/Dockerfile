FROM alpine:3.7

RUN apk --no-cache add \
    bash \
    less \
    ruby \
    ruby-irb \
    ruby-rdoc \
    shadow

RUN gem install \
        puppet \
        facter

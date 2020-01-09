FROM ruby:2.6.1-alpine3.9

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk add --update alpine-sdk icu-dev cmake openssl-dev
RUN gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/ && \
    gem install github-linguist gollum github-markdown

EXPOSE 80

WORKDIR /wiki

CMD ["gollum", "--port", "80"]

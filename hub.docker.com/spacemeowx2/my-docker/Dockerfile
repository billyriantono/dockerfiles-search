FROM ruby:2.5-alpine

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

WORKDIR /app

RUN gem install bundler

RUN apk add --no-cache --virtual .deps build-base git \
    && git clone https://owo.codes/Seriel/Yuuki-Bot.git \
    && cd Yuuki-Bot \
    && bundle install \
    && apk del .deps

RUN apk add --no-cache libsodium

WORKDIR /app/Yuuki-Bot/

CMD [ "sh", "/app/Yuuki-Bot/run_linux.sh" ]

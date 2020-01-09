FROM openjdk:8-jre-alpine
LABEL maintainer "CAMPFIRE, Inc.<tech@camp-fire.jp>"

# `libc6-compat` is needed to install `embulk-input-mysql`.
RUN apk --update --no-cache add libc6-compat tzdata ruby ruby-bundler ruby-json ruby-webrick && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  echo "Asia/Tokyo" > /etc/timezone && \
  apk del tzdata

RUN wget -q https://dl.digdag.io/digdag-latest -O /usr/local/bin/digdag && \
  chmod +x /usr/local/bin/digdag && \
  wget -q https://dl.embulk.org/embulk-latest.jar -O /usr/local/bin/embulk && \
  chmod +x /usr/local/bin/embulk && \
  adduser --shell /sbin/nologin --disabled-password --gecos "" digdag

WORKDIR /home/digdag

ENV PATH=${PATH}:/usr/local/bin

COPY tasks tasks
COPY notify_templates notify_templates
COPY config config
COPY scripts scripts
COPY main.dig .

RUN embulk gem install embulk-input-mysql embulk-output-mysql embulk-filter-mask

EXPOSE 65432

CMD ["java", "-jar", "/usr/local/bin/digdag", "run", "main.dig"]

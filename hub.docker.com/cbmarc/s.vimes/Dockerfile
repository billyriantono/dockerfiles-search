FROM alpine:3.7

RUN apk --no-cache add \
  # Install NodeJS:
  nodejs \
  # Install ffmpeg for video recording:
  ffmpeg \
  && npm install -g \
  # Install Nightwatch.js:
  nightwatch@1.1.0 \
  && npm install -g \
  # Add nightwatch-video-recorder globally:
  nightwatch-video-recorder@'2.0.0' \
  # Clean up obsolete files:
  && rm -rf \
  /tmp/* \
  /root/.npm

RUN adduser -D -u 1000 node && \
        mkdir -p /opt/node && \
        chown -R node:node /opt/node

USER node

WORKDIR /home/node

COPY wait-for.sh /usr/local/bin/wait-for
COPY entrypoint.sh /usr/local/bin/entrypoint
COPY run-nightwatch.sh /usr/local/bin/run-nightwatch
ENTRYPOINT ["entrypoint"]

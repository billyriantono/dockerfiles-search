FROM frolvlad/alpine-glibc:latest

RUN set -eux; \
    wget -qO factorio.tar.xz https://www.factorio.com/get-download/latest/headless/linux64; \
    tar Jxf factorio.tar.xz; \
    rm -f factorio.tar.xz; \
    ( echo '{'; \
      echo '  "name": "Factorio LAN Server",'; \
      echo '  "description": "Factorio LAN Server",'; \
      echo '  "visibility": { "lan": true },'; \
      echo '  "require_user_verification": false,'; \
      echo '  "allow_commands": "true",'; \
      echo '  "autosave_interval": 60,'; \
      echo '  "autosave_slots": 1,'; \
      echo '  "auto_pause": false,'; \
      echo '  "non_blocking_saving": true'; \
      echo '}'; \
    ) > /factorio/data/server-settings.json

VOLUME ["/factorio/saves"]

CMD ["/factorio/bin/x64/factorio", "--start-server-load-latest", "--server-settings", "/factorio/data/server-settings.json"]

EXPOSE 34197/udp

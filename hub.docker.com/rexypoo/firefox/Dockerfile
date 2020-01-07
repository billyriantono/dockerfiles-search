FROM ubuntu AS build

# Install prerequisites
RUN apt-get update && apt-get install -yq \
    apulse \
    ca-certificates \
    dbus-x11 \
    firefox \
    hicolor-icon-theme \
    libasound2 \
    libcanberra-gtk3-module \
    libgl1-mesa-dri \
    libgl1-mesa-glx \
    libpulse0 \
    --no-install-recommends \
 && rm -rf /var/lib/apt/lists/*

# To patch audio we need some extra code
COPY firefox-helper.sh /usr/local/bin/firefox-helper.sh
RUN chmod a+x /usr/local/bin/firefox-helper.sh

FROM build AS drop-privileges
# Create user
ENV USER=firefox \
    UID=24322 \
    TEMPLATE=/firefox/Downloads
# Whoever owns /firefox/Downloads owns the instance

WORKDIR /firefox

RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "$(pwd)" \
    --no-create-home \
    --uid "$UID" \
    "$USER" \
 && adduser "$USER" audio \
 && mkdir /firefox/Downloads \
 && chown -R "$USER":"$USER" .

ADD https://raw.githubusercontent.com/Rexypoo/docker-entrypoint-helper/master/entrypoint-helper.sh /usr/local/bin/entrypoint-helper.sh
RUN chmod u+x /usr/local/bin/entrypoint-helper.sh
ENTRYPOINT ["entrypoint-helper.sh", "/usr/local/bin/firefox-helper.sh", "--no-remote"]

FROM drop-privileges AS configure

# Modify firefox defaults
RUN echo 'pref("general.config.obscure_value", 0);' >> /usr/lib/firefox/defaults/pref/local-settings.js \
 && echo 'pref("general.config.filename", "mozilla.cfg");' >> /usr/lib/firefox/defaults/pref/local-settings.js \
 && echo "//" > /usr/lib/firefox/mozilla.cfg \ 
 && echo 'pref("browser.tabs.remote.autostart", false);  // Disable multithreading that breaks docker' >> /usr/lib/firefox/mozilla.cfg \
 && echo 'pref("app.normandy.first_run", false);  // Disable first-time setup' >> /usr/lib/firefox/mozilla.cfg

FROM configure AS dev
ENTRYPOINT ["bash"]

FROM configure AS release

LABEL org.opencontainers.image.url="https://hub.docker.com/r/rexypoo/firefox" \
      org.opencontainers.image.documentation="https://hub.docker.com/r/rexypoo/firefox" \
      org.opencontainers.image.source="https://github.com/Rexypoo/docker-firefox" \
      org.opencontainers.image.version="0.1a" \
      org.opencontainers.image.licenses="MIT" \
      org.opencontainers.image.description="Firefox on Docker" \
      org.opencontainers.image.title="rexypoo/firefox" \
      org.label-schema.docker.cmd='mkdir -p "$HOME"/.firefox-settings && \
      docker run -d --rm \
      --name firefox \
      --net=host \
      -e DISPLAY \
      -v /tmp/.X11-unix:/tmp/.X11-unix:ro \
      --device /dev/snd \
      -v "$HOME"/Downloads:/firefox/Downloads \
      -v "$HOME"/.firefox-settings:/firefox/.mozilla/firefox \
      rexypoo/firefox' \
      org.label-schema.docker.cmd.devel="docker run -it --rm --entrypoint bash rexypoo/firefox" \
      org.label-schema.docker.cmd.debug="docker exec -it firefox bash"

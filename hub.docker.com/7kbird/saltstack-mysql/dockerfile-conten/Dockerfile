# tibia-docker
# Dockerfile based on Ubuntu 18 and OpenSSL 1.0.2

FROM shamelesscookie/openssl:1.0.2
LABEL \
  MAINTAINER="Nick Laurent aka Witches Moon" \
  DESCRIPTION="Docker image to run the Tibia Linux Client 11 on modern distributions with new versions of OpenSSL." \
  REQUIREMENTS="Docker. Use the build-image.sh script to build this image, and set up the Tibia client files as Docker volumes." \
  USAGE="docker run --rm --privileged --name tibia-client -e "DISPLAY=$DISPLAY" -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" --mount source="tibia-client-volume",target="/usr/local/bin" --mount source="tibia-settings-volume",target="/home/tibia_player/.local/share" tibia-docker"

# Add the Tini init controller to allow the container to exit gracefully.
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini

# Create a non-root user; install OpenGL, QT5 and GPG; validate Tini.
RUN \
  set -ex ;\
  
  # Set up the user
  useradd -ms /bin/bash tibia_player ;\
  mkdir -p /usr/local/bin/Tibia /home/tibia_player/.local/share ;\
  chown tibia_player:tibia_player /usr/local/bin/Tibia /home/tibia_player/.local/share ;\
  
  # Install packages
  chmod +x /tini ;\
  apt update -y ;\
  apt install -y --no-install-recommends mesa-utils libgl1-mesa-glx ttf-mscorefonts-installer ;\
  apt install -y --install-recommends qt5-default ;\

  # Clean up
  apt autoremove --purge --yes ;\
  apt clean ;\
  rm -rf /var/lib/apt/lists/*

USER tibia_player
WORKDIR "/usr/local/bin/Tibia"
ENTRYPOINT ["/tini", "--"]
CMD ["/bin/bash", "-c", "set -e && ./start-tibia-launcher.sh && tail -f /dev/null"]

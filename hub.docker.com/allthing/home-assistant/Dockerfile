# Notice:
# When updating this file, please also update virtualization/Docker/Dockerfile.dev
# This way, the development image and the production image are kept in sync.

FROM python:3.6
LABEL maintainer="Paulus Schoutsen <Paulus@PaulusSchoutsen.nl>"

# Uncomment any of the following lines to disable the installation.
#ENV INSTALL_TELLSTICK no
#ENV INSTALL_OPENALPR no
#ENV INSTALL_FFMPEG no
#ENV INSTALL_LIBCEC no
#ENV INSTALL_SSOCR no
#ENV INSTALL_IPERF3 no

VOLUME /config

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Copy build scripts
COPY virtualization/Docker/ virtualization/Docker/
RUN virtualization/Docker/setup_docker_prereqs

# Install hass component dependencies
COPY requirements_all.txt requirements_all.txt
# Uninstall enum34 because some dependencies install it but breaks Python 3.4+.
# See PR #8103 for more info.
RUN pip3 install --no-cache-dir -r requirements_all.txt && \
    pip3 install --no-cache-dir mysqlclient psycopg2 uvloop cchardet cython

# Copy source
COPY . .

#CMD [ "python", "-m", "homeassistant", "--config", "/config" ]

#FROM homeassistant/home-assistant:0.74.2
#ARG userid
#ARG username
#RUN useradd --no-create-home --user-group --shell /bin/bash --uid $userid $username 
#RUN pip3 install -U ptvsd==3.0.0 # For debugging with VS Code. 
COPY config/ /config/
# This has to be in the shell form. (Not array) https://www.ctl.io/developers/blog/post/dockerfile-entrypoint-vs-cmd/
# Alternative: https://github.com/waisbrot/docker-wait
# I Have to put the sleep in because MQTT is slow to start.
CMD sleep 15 && python -m homeassistant --config /config 

# TODO: Need to prevent start until MQTT is up:
# https://docs.docker.com/compose/startup-order/
FROM     python:3.5-alpine

ARG      DOCKER_UID

# Create a user to run the application
# RUN      adduser -D -u ${DOCKER_UID} flexget
WORKDIR  /home/flexget

# Data and config volumes
VOLUME   /config
VOLUME   /downloads

# Install FlexGet
RUN      pip3 install -U --index-url https://pypi.douban.com/simple pip && pip3 install --index-url https://pypi.douban.com/simple flexget

# Add start script
COPY     start.sh /home/flexget/
RUN      chmod +x ./start.sh
ENV      WEB_PASSWORD 123456
EXPOSE   5050
CMD      ["./start.sh"]
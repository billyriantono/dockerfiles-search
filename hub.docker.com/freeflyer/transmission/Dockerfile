FROM alpine
RUN apk add --no-cache bash
RUN apk add --no-cache transmission-daemon
RUN mkdir /downloads

# Add default config 
COPY files/settings.json /etc/transmission/settings.json
COPY files/entrypoint.sh /bin/entrypoint.sh

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["/bin/entrypoint.sh"]

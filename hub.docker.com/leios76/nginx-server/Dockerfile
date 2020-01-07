# Pull base image.
FROM leios76/nginx-volume:1.4.6-1

COPY files/init.sh /init.sh

# Define default command.
CMD ["/init.sh"]

# Define working directory.
WORKDIR /etc/nginx

# Expose ports.
EXPOSE 80

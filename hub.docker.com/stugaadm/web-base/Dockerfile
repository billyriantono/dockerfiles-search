FROM gliderlabs/alpine

MAINTAINER StugA-Admins <stuga-adm@fb3.uni-bremen.de>

# Set username and home directory
ENV USER_NAME www
ENV DATA /var/www-data
ENV HTDOCS /var/www

RUN apk --update upgrade

# Install common packages
RUN apk add vsftpd tzdata

# Create user
RUN adduser -D -h $DATA $USER_NAME

# Set up htdocs directory
RUN mkdir -p $DATA/htdocs
RUN ln -s $DATA/htdocs $HTDOCS
RUN chown -R $USER_NAME:$USER_NAME $DATA

# Set current directory to home dir
WORKDIR $HTDOCS

EXPOSE 8080

# Set current user
USER $USER_NAME

ONBUILD USER root

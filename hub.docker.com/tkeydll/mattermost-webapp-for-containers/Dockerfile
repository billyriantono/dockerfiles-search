# Copyright (c) 2016 Mattermost, Inc. All Rights Reserved.
# See License.txt for license information.
FROM tkeydll/mysql:5.7

# Install ca-certificates to support TLS of Mattermost v3.5
RUN apt-get update && apt-get install -y ca-certificates

#
# Configure SQL
#

ENV MYSQL_ROOT_PASSWORD=mostest
ENV MYSQL_USER=mmuser
ENV MYSQL_PASSWORD=mostest
ENV MYSQL_DATABASE=mattermost_test

#
# Configure Mattermost
#
WORKDIR /home/mm

# Copy over files
ADD https://releases.mattermost.com/4.3.1/mattermost-team-4.3.1-linux-amd64.tar.gz .
RUN tar -zxvf ./mattermost-team-4.3.1-linux-amd64.tar.gz
ADD config_docker.json ./mattermost/config/config_docker.json
ADD docker-entry.sh .

RUN chmod +x ./docker-entry.sh
ENTRYPOINT ./docker-entry.sh

RUN rm ./mattermost-team-4.3.1-linux-amd64.tar.gz

VOLUME /home/mm

# Ports
EXPOSE 8065

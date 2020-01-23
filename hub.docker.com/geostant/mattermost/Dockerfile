FROM ubuntu:18.04

COPY mattermost/ /opt/mattermost

RUN mkdir /opt/mattermost/data; \
    useradd --system --user-group mattermost; \
    chown -R mattermost:mattermost /opt/mattermost; \
    chmod -R g+w /opt/mattermost

EXPOSE 8065

COPY entrypoint /usr/local/bin/
CMD ["entrypoint"]

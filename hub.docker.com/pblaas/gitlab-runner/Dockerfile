FROM gitlab/gitlab-runner:latest

ADD entrypoint /
RUN chmod +x /entrypoint

ADD config.json /root/.docker/config.json


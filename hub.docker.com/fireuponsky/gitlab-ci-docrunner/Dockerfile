FROM sameersbn/gitlab-ci-runner:latest
MAINTAINER hugo@188.com

RUN apt-get update && \
    apt-get install -y fontconfig && \
    rm -rf /var/lib/apt/lists/*

ADD apt-source/ /root/apt-source/
RUN cat /root/apt-source/sources.list > /etc/apt/sources.list

ADD env/ /root/env/
RUN cat /root/env/bashrc >> /home/gitlab_ci_runner/.bashrc && \
    cat /root/env/bashrc >> /home/gitlab_ci_runner/.profile

ADD begin/ /app/begin
RUN chmod -R 755 /app/begin

ENTRYPOINT ["/app/begin/begin.sh"]
CMD ["app:start"]

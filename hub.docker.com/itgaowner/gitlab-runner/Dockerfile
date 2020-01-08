FROM gitlab/gitlab-runner:latest
RUN apt-get update
RUN apt-get install -y ca-certificates
RUN cp /usr/share/ca-certificates/mozilla/* /etc/ssl/certs/

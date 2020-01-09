FROM blackikeeagle/alpine:stable
MAINTAINER Ike Devolder, ike.devolder@gmail.com

COPY ./root /

WORKDIR /work/

ENV DOCKER_HOST unix:///var/run/docker.sock

CMD ["docker-developer-hosts"]

# Based on https://docs.docker.com/engine/examples/apt-cacher-ng/
# Build: docker build -t akatiyar/apt-cacher .
# Run: docker run --name apt-cacher -h apt-cacher  -d -p 3142:3142 -v /var/cache/apt-cacher-ng:/var/cache/apt-cacher-ng akatiyar/apt-cacher
#
# and then you can build container with:
# docker build --build-arg http_proxy="http://192.168.0.112:3142" -t akatiyar/freenect2ros_cudnn:new .
#
# or run containers with:
#   docker run -t -i --rm -e http_proxy http://dockerhost:3142/ debian bash
#
# Here, `dockerhost` is the IP address or FQDN of a host running the Docker daemon
# which acts as an APT proxy server.
#
# You can start/stop apt-cacher, however, if you remove it or run with "--rm",
# you will not be able to use cache.

FROM ubuntu:16.04

VOLUME ["/var/cache/apt-cacher-ng"]

RUN apt-get update && apt-get install -y apt-cacher-ng

EXPOSE 3142
CMD chmod 777 /var/cache/apt-cacher-ng && /etc/init.d/apt-cacher-ng start && tail -f /var/log/apt-cacher-ng/*

FROM tobiashofmann/openui5-rt:1.34
MAINTAINER Tobias Hofmann <tobi...@gmail.com>
WORKDIR /tmp/openui5
RUN git fetch
# build and install openui5 versions 1.36
RUN curl -sL https://raw.githubusercontent.com/tobiashofmann/docker-openui5-rt/1.36/create.sh | bash -
EXPOSE 80
ENTRYPOINT /usr/sbin/apache2ctl -D FOREGROUND

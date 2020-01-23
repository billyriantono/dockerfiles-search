FROM autodomotalus/base

MAINTAINER Autodomotalus <https://github.com/autodomotalus>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -qq update
RUN apt-get install -y nodejs npm

VOLUME ["/data"]

ADD . /data
#RUN cd /data && npm install

EXPOSE 8888

WORKDIR /data

# Define default command.
CMD ["bash"]

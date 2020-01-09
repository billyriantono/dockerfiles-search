FROM debian:jessie
MAINTAINER Goran Mekić <meka@lugons.org>

ADD . /app
RUN /app/bin/build.sh
CMD /app/bin/run.sh
VOLUME /ahrimana
EXPOSE 8000 9000

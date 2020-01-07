# OMD-Labs-Edition with Grafana

# Run:
# $ docker run -it --rm -p 80:80 -p 443:443 -h omd haxx0r07/omd-grafana

# browser: 127.0.0.1/default
# user: omdadmin
# pass: omd
# It takes a few seconds till the first performance data is created.

FROM debian:8

MAINTAINER haxx0r07@gmail.com

RUN gpg --keyserver keys.gnupg.net --recv-keys F8C1CA08A57B9ED7
RUN gpg --armor --export F8C1CA08A57B9ED7 | apt-key add -
RUN echo 'deb http://labs.consol.de/repo/stable/debian jessie main' >> /etc/apt/sources.list

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y omd-labs-edition net-tools iputils-ping

RUN omd create default
RUN omd config default set TMPFS off
RUN omd config default set INFLUXDB on
RUN omd config default set NAGFLUX on
RUN omd config default set GRAFANA on
RUN omd config default set CORE icinga2
RUN omd config default set PNP4NAGIOS off
RUN sed -i -e s/host-pnp/host-perf/g /omd/sites/default/etc/icinga2/conf.d/hosts.conf

EXPOSE 80 443 8086

COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
RUN sed -i 's/\r//' /entrypoint.sh #Just for Windows systems...

COPY ./services.conf /omd/sites/default/etc/icinga2/conf.d/services.conf
COPY ./commands.conf /omd/sites/default/etc/icinga2/conf.d/commands.conf

ENTRYPOINT ["/entrypoint.sh"]

FROM debian:jessie
MAINTAINER Roberto Quintanilla <roberto.quintanilla@gmail.com>

# Add the kibana user and group first to make sure their IDs get assigned
# consistently (we like it to be 1000), regardless of whatever dependencies get
# added:
RUN cp /etc/default/useradd /etc/default/useradd.bak \
  && echo "HOME=" >> /etc/default/useradd \
  && useradd --create-home --shell /usr/sbin/nologin kibana \
  && rm -rf /etc/default/useradd \
  && mv /etc/default/useradd.bak /etc/default/useradd \
  && rm /kibana/.bash_logout /kibana/.bashrc /kibana/.profile

# Set the Kibana Version:
ENV KIBANA_VERSION 4.0.1

# Fetch Kibana:
# - Install curl so we can fetch the kibana code
# - Fetch the Kibana code to the kibana home directory (/kibana)
# - Fetch a default kibana configuration file - which should be customized for running as a Docker container, if applies...
# - Fetch an nginx configuration customized to run exclusively the kibana 3 app
# - Uninstall curl & curl dependencies, as it is no longer required.
RUN  apt-get update && apt-get install -y curl ca-certificates --no-install-recommends \
  && curl -SL "https://download.elasticsearch.org/kibana/kibana/kibana-$KIBANA_VERSION-linux-x64.tar.gz" \
  | tar -xzC /kibana --strip-components=1 \
  && curl -SL "https://raw.githubusercontent.com/vovimayhem/docker-kibana/master/kibana4/config/kibana.yml" \
  > /kibana/config/kibana.yml \
  && apt-get remove -y curl ca-certificates && apt-get -y autoremove \
  && rm -rf /var/lib/apt/lists/*

# Change the Kibana installation files owner to elasticsearch:
RUN chown -R kibana:kibana /kibana

# Set mountable volume:
VOLUME ["/kibana/config"]

# Add kibana bin directory to path:
ENV PATH /kibana/bin:$PATH

USER kibana
WORKDIR /kibana

# Expose Kibana UI port:
EXPOSE 5601

# Define default command.
CMD ["kibana"]

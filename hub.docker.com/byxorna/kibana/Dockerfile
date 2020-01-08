FROM debian:latest
MAINTAINER Gabe Conradi <gummybearx@gmail.com>
ENV KIBANA_VERSION 4.0.1
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
RUN curl -SL https://download.elasticsearch.org/kibana/kibana/kibana-${KIBANA_VERSION}-linux-x64.tar.gz | \
  tar xzC /opt
RUN ln -s /opt/kibana-${KIBANA_VERSION}-linux-x64/config/kibana.yml /etc/kibana.yml
ENV PATH /opt/kibana-${KIBANA_VERSION}-linux-x64/bin:$PATH
WORKDIR /opt/kibana-${KIBANA_VERSION}-linux-x64
EXPOSE 80
ENTRYPOINT ["kibana","--port","80"]
CMD ["--config","/etc/kibana.yml"]

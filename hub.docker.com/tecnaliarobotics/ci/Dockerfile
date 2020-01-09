FROM ubuntu:trusty

RUN apt-get update && apt-get install -y squid-deb-proxy-client && rm -rf /var/lib/apt/lists/*

RUN echo 'Acquire::http::Proxy "http://172.18.0.2:8000";' > /etc/apt/apt.conf.d/30autoproxy

FROM ubuntu
MAINTAINER Zloy Rabadaber <zrabadaber@gmail.com>

ADD nomad /usr/bin/nomad

# Expose http, rpc and serf ports
EXPOSE 4646
EXPOSE 4647
EXPOSE 4648

CMD ["nomad", "agent", "-dev"]


FROM tsuru/static:latest

ADD . /home/application/current
ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

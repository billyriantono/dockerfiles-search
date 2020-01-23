from gitlab/gitlab-runner:latest
maintainer Alexander Schittler <a.schittler@77ps.de>

env DEBIAN_FRONTEND=noninteractive

run apt-get update
run apt-get install -y curl
run sh -c "wget -qO- https://get.docker.com/ | sh"

#run curl -L https://github.com/kelseyhightower/confd/releases/download/v0.10.0/confd-0.10.0-linux-amd64 > /usr/local/bin/confd
#run chmod +x /usr/local/bin/confd

run curl -L https://github.com/docker/compose/releases/download/1.5.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
run chmod +x /usr/local/bin/docker-compose

run mkdir -p /etc/confd/conf.d
run mkdir -p /etc/confd/templates

add ./confme /confme
run chmod +x /confme

add ./conf.d /etc/confd/conf.d
add ./templates /etc/confd/templates

ENTRYPOINT ["/bin/bash"]
CMD ["/confme"]

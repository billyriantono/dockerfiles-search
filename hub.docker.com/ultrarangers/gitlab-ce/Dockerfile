FROM gitlab/gitlab-ce:latest
LABEL MAINTAINER hub.docker.com/la1255

# TODO add default volume args?
# TODO add default 

# Start using:
# $ sudo docker run --detach \
#   --hostname gitlab.local \
#   --publish 10040:443 --publish 10041:80 --publish 22:22 \
#   --name gitlab \
#   --restart always \
#   --volume /Users/$(whoami)/gitlab/config:/etc/gitlab:Z \
#   --volume /Users/$(whoami)/gitlab/logs:/var/log/gitlab:Z \
#   --volume /Users/$(whoami)/gitlab/data:/var/opt/gitlab:Z \
#   ultrarangers/gitlab-ce:latest
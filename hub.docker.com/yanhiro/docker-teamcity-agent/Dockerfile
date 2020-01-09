#inherit from fwfa's base debian img
FROM yanhiro/docker-java
MAINTAINER yanhiro <fjallot@fwfa-consulting.com>

ENV TEAMCITY_HOSTNAME teamcity
ENV TEAMCITY_PORT 8111

ADD setup-agent.sh /scripts/setup-agent.sh

RUN apt-get update && apt-get install -y unzip sudo docker
RUN adduser teamcity

VOLUME /var/lib/docker
EXPOSE 9090
CMD service docker start; sudo -u teamcity -s -- sh -c "TEAMCITY_HOSTNAME=${TEAMCITY_HOSTNAME} TEAMCITY_PORT=${TEAMCITY_PORT} bash /scripts/setup-agent.sh"
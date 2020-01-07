FROM gocd/gocd-agent-ubuntu-16.04:v17.11.0

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install build-essential libssl-dev -y \
 && curl -sL "https://deb.nodesource.com/setup_8.x" | bash - \
 && apt-get install nodejs -y

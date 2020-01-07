FROM gocd/gocd-agent

RUN apt-get update && apt-get install -y curl
RUN curl -fsSL https://get.docker.com/ | sh
RUN usermod -aG docker go

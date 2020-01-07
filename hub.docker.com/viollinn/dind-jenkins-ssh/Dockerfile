FROM jenkins/ssh-slave
RUN  curl -sSL https://get.docker.com/ | sh
RUN apt-get update &&\    
    apt-get clean -y && rm -rf /var/lib/apt/lists/*
    
RUN curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose &&\
    chmod +x /usr/local/bin/docker-compose

# SMB and SSH clients in Ubuntu
# 
# Andrew Hills (a.hills@sheffield.ac.uk)

FROM ubuntu:latest

RUN ln -fs /usr/share/zoneinfo/Europe/London /etc/localtime
RUN sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
    apt update && \
    apt -y upgrade && \
    apt install -y byobu curl git htop man unzip vim wget smbclient && \
    apt install -y openssh-client git-lfs && \
    rm -rf /var/lib/apt/lists/*
RUN mkdir -p ~/.ssh && \
    chmod 700 ~/.ssh
RUN bash -c "echo -e 'Host *\n\tStrictHostKeyChecking no\n\n' > ~/.ssh/config"

CMD ["/bin/bash"]

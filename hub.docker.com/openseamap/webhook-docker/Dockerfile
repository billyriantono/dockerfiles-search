FROM phusion/baseimage:0.9.19
MAINTAINER Axel Utech <axel@brasshack.de>

ENV LANG en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive


RUN \
    echo "Acquire::Languages \"none\";\nAPT::Install-Recommends \"true\";\nAPT::Install-Suggests \"false\";" > /etc/apt/apt.conf ;\
    echo "Europe/Berlin" > /etc/timezone && dpkg-reconfigure tzdata ;\
    locale-gen en_US.UTF-8 en_DK.UTF-8 de_DE.UTF-8 ;\
    apt-get -q -y update

RUN \
    apt-get install -y python3 python3-pip netcat openssh-client git curl docker.io ;\
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN git clone https://github.com/aAXEe/github-webhook-handler.git /usr/src/app


WORKDIR /usr/src/app

RUN python3 -m pip install -U pip
RUN python3 -m pip install --no-cache-dir -r requirements.txt

RUN mkdir /data


ENV FLASK_GITHUB_WEBHOOK_REPOS_JSON=/data/repos.json
ENV FLASK_GITHUB_WEBHOOK_GITHUB_TOKEN=/data/github_token

CMD ["/sbin/my_init", "python3", "./index.py", "80"]
EXPOSE 80

VOLUME "/data"
VOLUME "/usr/src/app"

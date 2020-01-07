FROM openjdk:8
MAINTAINER vincent@autistici.org

RUN wget -P /tmp https://github.com/rundeck/rundeck-cli/releases/download/v0.1.23/rundeck-cli_0.1.23-1_all.deb
RUN dpkg -i /tmp/rundeck-cli_0.1.23-1_all.deb
RUN useradd -ms /bin/bash rundeck
USER rundeck
WORKDIR /home/rundeck

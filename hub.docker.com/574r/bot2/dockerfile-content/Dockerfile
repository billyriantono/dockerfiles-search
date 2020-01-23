FROM ubuntu:16.04

#ENV http_proxy "http://proxy.materna.de:8080"
#ENV https_proxy "http://proxy.materna.de:8080"

RUN apt-get update && apt-get install --yes \
    apt-utils \
    sudo \
    make \
    gcc-avr \
    binutils \
    avr-libc \
    avrdude \
    arduino-mk \
    python-pip \
    python3-dev \
    nano
RUN pip install --upgrade pip
RUN pip install pyserial

USER root

RUN useradd -ms /bin/bash dragana
RUN adduser dragana dialout
RUN adduser dragana uucp

USER dragana
RUN  mkdir -p /home/dragana/Dokumente/repos_git/modules/config/configurationsystem/Arduino_Docker_Blink

USER root
COPY . /home/dragana/Dokumente/repos_git/modules/config/configurationsystem/Arduino_Docker_Blink
#RUN chown root:root /etc/sudoers && chmod 440 /etc/sudoers
#COPY . /usr/

#COPY . /etc/sudoers
#RUN chown root:root /etc/sudoers && chmod 440 /etc/sudoers

#RUN chmod +x /home/dragana/Dokumente/repos_git/modules/config/configurationsystem/Arduino_Docker_Blink/run.sh

#CMD /home/dragana/Dokumente/repos_git/modules/config/configurationsystem/Arduino_Docker_Blink/run.sh

#CMD while true; do sleep 1000; done
#WORKDIR /home/dragana/Dokumente/repos_git/modules/config/configurationsystem/Arduino_Docker_Blink/
#CMD /home/dragana/Dokumente/repos_git/modules/config/configurationsystem/Arduino_Docker_Blink/run.sh
#CMD make upload

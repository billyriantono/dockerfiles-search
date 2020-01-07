# --- this is ubuntu trusty 14.04 ----
FROM phusion/baseimage 
MAINTAINER Adrian Stachurski <astachurski@gmail.com>

RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh
RUN apt-get update && apt-get install -y -q unzip openjdk-7-jre-headless git

RUN mkdir /etc/service/go-agent
ADD gocd-agent-start.sh /etc/service/go-agent/run
ADD http://download.go.cd/gocd-deb/go-agent-15.2.0-2248.deb /tmp/go-agent.deb

WORKDIR /tmp
RUN dpkg -i /tmp/go-agent.deb
RUN sed -i 's/DAEMON=Y/DAEMON=N/' /etc/default/go-agent

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# --- below can be changed by external injection or changed in place ---
ENV OTP_VERSION "17.5"
ENV OTP_VERSION_NAME "OTP175"
ENV PRESET_NAME_KEY ssh-key-name
# -end-- below can be changed by external injection or changed in place ---

ENV HOME /var/go

RUN sudo adduser --quiet --system --shell /bin/sh --group mongooseim &&\
    sudo apt-get update &&\
    sudo apt-get install -y -q make &&\
    sudo apt-get install -y -q build-essential dh-make libncurses5-dev openssl libssl-dev fop xsltproc unixodbc-dev &&\
    sudo apt-get install -y -q libexpat1-dev

RUN sudo apt-get install -y -q curl &&\
    curl -O -s https://raw.githubusercontent.com/spawngrid/kerl/master/kerl &&\
    chmod a+x kerl &&\
    cp kerl /usr/bin

RUN ./kerl update releases &&\
    ./kerl build ${OTP_VERSION} ${OTP_VERSION_NAME} &&\
    ./kerl install ${OTP_VERSION_NAME} /usr/${OTP_VERSION_NAME}

WORKDIR /var/go
ENV PATH $PATH:/usr/${OTP_VERSION_NAME}:/usr/${OTP_VERSION_NAME}/bin
USER go
RUN touch /var/go/.bashrc
USER go

RUN echo ". /usr/${OTP_VERSION_NAME}/activate" >> /var/go/.bashrc &&\
    echo "export PATH=$PATH:/usr/${OTP_VERSION_NAME}/bin" >> /var/go/.bashrc &&\
    echo "PATH=$PATH:/usr/${OTP_VERSION_NAME}" >> /var/go/.bashrc &&\
    echo "export TERM=xterm-256color" >> /var/go/.bashrc &&\
    echo "alias ll='ls -al'" >> /var/go/.bashrc

RUN mkdir .ssh &&\
    ssh-keygen -b 2048 -t rsa -f .ssh/${PRESET_NAME_KEY} -q -N "" &&\
    touch /var/go/.ssh/config &&\
    echo "Host backendhost" >> /var/go/.ssh/config &&\
    echo "user go" >> /var/go/.ssh/config &&\
    echo "Hostname 10.100.10.57" >> /var/go/.ssh/config &&\
    echo "IdentityFile /var/go/.ssh/${PRESET_NAME_KEY}" >> /var/go/.ssh/config

USER root
RUN sudo apt-get install -y -q emacs24

#RUN sudo apt-get install -y -q wget
#WORKDIR /var/lib/go-server/plugins/external
#RUN wget https://github.com/ashwanthkumar/gocd-build-github-pull-requests/releases/download/v1.2.3/gith#ub-pr-poller-1.2.3.jar

USER root
CMD ["/sbin/my_init"]




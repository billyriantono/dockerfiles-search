FROM phusion/baseimage:0.9.16
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


ENV OTP_VERSION "17.4"
ENV OTP_VERSION_NAME "OTP_174"
ENV HOME /var/go


RUN sudo apt-get update &&\
    sudo apt-get install -y -q make &&\
    sudo apt-get install -y -q build-essential libncurses5-dev openssl libssl-dev fop xsltproc unixodbc-dev &&\
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
    echo "export TERM=xterm-256color" >> /var/go/.bashrc 
RUN mkdir .ssh &&\
    ssh-keygen -b 2048 -t rsa -f .ssh/sshkey -q -N ""

USER root
RUN sudo apt-get install -y -q emacs24
USER root
CMD ["/sbin/my_init"]




FROM ubuntu:latest

MAINTAINER Chuan.C

#Setup host
#RUN echo $(head -1 /etc/hosts | cut -f1) call-work-host >> /etc/hosts
#RUN echo $(grep $(hostname) /etc/hosts | cut -f1) $HOSTNAME >> /etc/hosts
#sync time with local host : docker run -v /etc/localtime:/etc/localtime:ro

#Install basic packages
RUN apt-get update && apt-get install -y csh ssh git sudo language-pack-en libc6-i386

#Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/mobilis && \
    echo "mobilis:x:${uid}:${gid}:Mobilis,,,:/home/mobilis:/bin/bash" >> /etc/passwd && \
    echo "mobilis:x:${uid}:" >> /etc/group && \
    echo "mobilis ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/mobilis && \
    chmod 0440 /etc/sudoers.d/mobilis && \
    chown ${uid}:${gid} -R /home/mobilis

#Replace 1001 with your user / group id
RUN export uid=1001 gid=1001 && \
    mkdir -p /home/builder && \
    echo "builder:x:${uid}:${gid}:Builder,,,:/home/builder:/bin/bash" >> /etc/passwd && \
    echo "builder:x:${uid}:" >> /etc/group && \
    echo "builder ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/builder && \
    chmod 0440 /etc/sudoers.d/builder && \
    chown ${uid}:${gid} -R /home/builder

#Setup enviroinment for builder
USER builder
ENV B_HOME /home/builder

ADD apache-ant-1.9.6 $B_HOME/apache-ant-1.9.6
ADD apache-maven-3.3.3 $B_HOME/apache-maven-3.3.3
ADD javaswitch.sh $B_HOME/javaswitch.sh
ADD jdk1.5.0_22 $B_HOME/jdk1.5.0_22
ADD jdk1.7.0_80 $B_HOME/jdk1.7.0_80
ADD jdk1.8.0_60 $B_HOME/jdk1.8.0_60

COPY bash_logout $B_HOME/.bash_logout
COPY mkshrc $B_HOME/.mkshrc
COPY profile $B_HOME/.profile
COPY builder/bashrc.info $B_HOME/.bashrc

#Set evnironment for mobilis
USER mobilis
ENV M_HOME /home/mobilis
COPY bash_logout $M_HOME/.bash_logout
COPY mkshrc $M_HOME/.mkshrc
COPY profile $M_HOME/.profile
COPY mobilis/bashrc.info $M_HOME/.bashrc

RUN sudo ln -s /home/mobilis/eclipse /usr/local/mobilis

#Final
USER root
RUN echo 'root:admin' | chpasswd 
RUN echo 'builder:mobilis' | chpasswd 
RUN echo 'mobilis:mobilis' | chpasswd 

RUN mkdir /var/run/sshd && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && echo "export VISIBLE=now" >> /etc/profile 

EXPOSE 22




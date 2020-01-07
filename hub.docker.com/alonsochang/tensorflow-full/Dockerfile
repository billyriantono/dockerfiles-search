FROM b.gcr.io/tensorflow/tensorflow-full
MAINTAINER Alonso <alonso842736@cht.com.tw>

RUN apt-get update -y && apt-get install sudo vim openssh-server git python-pip -y && apt-get clean all
RUN pip install supervisor

RUN mkdir /var/run/sshd
RUN echo 'root:changeme' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# set root ssh login workdir
RUN echo 'cd /usr/src/app' >> /root/.bash_profile

# == begin to set react workspace ==
EXPOSE 22 
COPY supervisord.conf /etc/supervisord.conf
WORKDIR /usr/src/app
# ====================================

CMD ["/usr/local/bin/supervisord", "-c", "/etc/supervisord.conf"]

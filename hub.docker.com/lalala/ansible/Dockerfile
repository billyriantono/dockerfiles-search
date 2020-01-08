
FROM ubuntu:trusty


# Install packages
ENV DEBIAN_FRONTEND noninteractive


# Set locale (fix the locale warnings)
RUN locale-gen --purge en_US.UTF-8 && \
	echo   'LANG="en_US.UTF-8"' > /etc/default/locale && \
	echo   'LANGUAGE="en_US:en"' >> /etc/default/locale && \
	echo "Asia/Jerusalem"  > /etc/timezone &&\
	dpkg-reconfigure --frontend noninteractive tzdata && \
	rm /etc/apt/sources.list && \
	mkdir /root/.ssh && \
	mkdir /var/run/sshd && \
	mkdir -p /var/log/supervisor


ADD stuff/sources.list /etc/apt/sources.list



RUN apt-get update -y  && \
    apt-get install --no-install-recommends -y openssh-server supervisor  \
					python-software-properties software-properties-common \
					nano vim curl \
					python-pip python-dev && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible  




#ssh
#ssh configs

ADD sshkey.pub /root/.ssh/authorized_keys
RUN chown root:root /root/.ssh/authorized_keys && \
	sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config




ADD stuff/supervisord.conf /etc/supervisor/conf.d/supervisord.conf



EXPOSE  22
CMD env | grep _ >> /etc/environment && /usr/bin/supervisord
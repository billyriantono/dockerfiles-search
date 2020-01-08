FROM kr3ssh/debian-rbenv
MAINTAINER Sergey Besedin "kr3ssh@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y ssh nodejs sudo nginx npm

# Dirty fix after stupid nodejs developers
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN mkdir /var/run/sshd

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

RUN echo 'root:root' | chpasswd

RUN useradd -m -s /bin/bash vagrant

# Configure SSH access
RUN mkdir -p /home/vagrant/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ== vagrant insecure public key" > /home/vagrant/.ssh/authorized_keys
RUN chown -R vagrant: /home/vagrant
RUN echo -n 'vagrant:vagrant' | chpasswd
RUN touch /home/vagrant/.hushlogin

# Enable passwordless sudo for vagrant
RUN mkdir -p /etc/sudoers.d && echo "vagrant ALL= NOPASSWD: ALL" > /etc/sudoers.d/vagrant && chmod 0440 /etc/sudoers.d/vagrant

RUN echo '\n\
alias rails="bundle exec rails"\n\
alias rake="bundle exec rake"\n\
' >> /home/vagrant/.bashrc

RUN /etc/init.d/nginx stop

#TODO: install postgresql and mongo clients
RUN apt-get clean

EXPOSE 80 22

# Dockerize ssh daemon. All further jobs will run through ssh session
CMD nginx && /usr/sbin/sshd -D

FROM rastasheep/ubuntu-sshd:18.04
RUN apt-get -y update --fix-missing

RUN apt-get -y install sudo rsync

RUN useradd -p '$1$fVEKshYX$yY1tE86ImB2qUHNTU1/oA/' test
RUN mkdir /home/test
RUN mkdir -m 700 /home/test/.ssh
RUN chown -R test /home/test
RUN echo "test ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/test
RUN chmod 0440 /etc/sudoers.d/test

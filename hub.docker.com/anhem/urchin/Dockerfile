FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

# install dependencies
RUN apt-get update && \
    apt-get install -y sudo wget unzip openjdk-11-jdk git maven ecryptfs-utils mhddfs samba samba-common-bin whois acl

# install chrome
RUN wget https://dl.google.com/linux/linux_signing_key.pub
RUN apt-key add linux_signing_key.pub
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list
RUN apt-get update && \
    apt-get install -y google-chrome-stable && \
    apt-get clean

# setup permissions
RUN echo "root ALL=(ALL) NOPASSWD:/usr/bin/sudo,/usr/sbin/adduser,/usr/sbin/useradd,/usr/sbin/deluser,/usr/sbin/addgroup,/usr/sbin/delgroup,/bin/chown,/usr/bin/passwd,/bin/mount,/bin/umount,/usr/bin/mhddfs,/etc/init.d/smbd,/bin/mkdir,/bin/rm,/usr/bin/setfacl,/usr/bin/chattr,/bin/cat" >> /etc/sudoers.d/urchin

# get project
WORKDIR workspace

# get project
RUN git clone https://github.com/anhem/urchin.git .

# resolve dependencies
RUN mvn dependency:resolve
RUN mvn dependency:resolve-plugins
RUN mvn clean install -DskipTests=true -B -V

ADD entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
#ENTRYPOINT ["tail", "-f", "/dev/null"]


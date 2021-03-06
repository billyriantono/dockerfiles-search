FROM debian:jessie

RUN DEBIAN_FRONTEND=noninteractive apt-get update -y && apt-get upgrade -y
RUN DEBIAN_FRONTEND=noninteractive apt install -y sudo openssh-server git locales
RUN locale-gen en_US.UTF-8
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales

# To avoid annoying "perl: warning: Setting locale failed." errors,
# do not allow the client to pass custom locals, see:
# http://stackoverflow.com/a/2510548/15677
RUN sed -i 's/^AcceptEnv LANG LC_\*$//g' /etc/ssh/sshd_config

RUN mkdir /var/run/sshd

ENV GITOLITE_HOME=/gitolite
RUN adduser --system --group --shell /bin/sh git
RUN mkdir -p ${GITOLITE_HOME}
RUN chown -R git:git ${GITOLITE_HOME}

RUN cd ${GITOLITE_HOME}; su git -c "git clone git://github.com/sitaramc/gitolite src";
RUN cd ${GITOLITE_HOME}/src; su git -c "git checkout tags/v3.6.6";
RUN cd ${GITOLITE_HOME}; su git -c "src/install -to ${GITOLITE_HOME}";

# https://github.com/docker/docker/issues/5892
RUN chown -R git:git ${GITOLITE_HOME}

# http://stackoverflow.com/questions/22547939/docker-gitlab-container-ssh-git-login-error
RUN sed -i '/session    required     pam_loginuid.so/d' /etc/pam.d/sshd

# Remove SSH host keys, so they will be generated by /init
RUN rm -f /etc/ssh/ssh_host_*

ADD ./entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh", "/usr/sbin/sshd", "-D"]

EXPOSE 22

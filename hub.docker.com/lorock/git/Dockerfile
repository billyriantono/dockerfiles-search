FROM  ubuntu:16.04
MAINTAINER Lorock.Xu "https://github.com/lorock"
RUN apt-get update \
&& apt-get install -y openssh-server git \
&& adduser git \
&& sed -i '/^git.*/d' /etc/passwd \
&& echo "git:x:1000:1000::/home/git:/usr/bin/git-shell" >> /etc/passwd \
&& mkdir /home/git/.ssh
COPY ./authorized_keys /home/git/.ssh/authorized_keys
RUN chown -R git.git /home/git/.ssh \
&& chmod 600 /home/git/.ssh/authorized_keys \
&& mkdir /lorock \
&& cd /lorock \
#初始化默认仓库git clone git@server:/lorock/lorock.git
&& git init --bare lorock.git \
&& chown -R git.git lorock.git \
&& mkdir /var/run/sshd \
&& echo 'root:root' |chpasswd \
&& echo 'git:lorock@gitserver' |chpasswd \
&& sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
&& sed -ri 's/^#AuthorizedKeysFile/AuthorizedKeysFile/g' /etc/ssh/sshd_config \
#&& sed -ri 's/^PermitEmptyPasswords no/PermitEmptyPasswords yes/g' /etc/ssh/sshd_config \
&& sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]

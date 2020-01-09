FROM centos

WORKDIR /root/

RUN yum install -y openssh-server
RUN mkdir -p /var/run/sshd
RUN mkdir -p /root/.ssh/
RUN echo 'ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA92kiZ6bfyyqgz75sWI26mZ8C8b2+a1uPOw9z9XUHKScK2sUmdgzTtPhPR8BN7s2dVA2koFUZLW717fVVFAVdEk141NF+YuMC4RGLKVycSdgG9DoYI6DESH+QLhgx1Nwod5oxxlU6TqxzN/9GP4G03Ycn8mvzaq7kLukYUWtEnTjg2yovg0cT521Enk9l1oarLFl9k29SW0pWCWk1W/A/X1vujnuM5Eb+UBYHow3mtTOcyWYM3uB3fryyshnSHuzzaHJM5CWA5CuxI3Q4husbgftY1ZLAcqMXUWYsRRdN9oaDsJ9ClwQ0WhmL2MHd0rDnaE85a5vvRuguNyQqi8w3Bw== 452125301@qq.com'>/root/.ssh/authorized_keys
RUN ssh-keygen -q -t rsa -b 2048 -f /etc/ssh/ssh_host_rsa_key -P '' -N ''

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo 'Asia/Shanghai' >/etc/timezone

EXPOSE 22

CMD /usr/sbin/sshd -D 

FROM pfadipatria/ruby-1.9.3

RUN apt-get update && \
 apt-get install openssh-server java7-runtime -y && \
 mkdir /var/run/sshd && \
 adduser jenkins && \
 echo "jenkins:jenkins" | chpasswd
 
EXPOSE 22

ENTRYPOINT ["/usr/sbin/sshd", "-D"]

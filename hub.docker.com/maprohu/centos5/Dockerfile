FROM centos:centos5
RUN yum -y install \
	java-1.7.0-openjdk \
	openssh-server 
	
RUN echo PermitEmptyPasswords yes >> /etc/ssh/sshd_config && \  
	echo PermitRootLogin yes >> /etc/ssh/sshd_config && \
	echo 'root:' | chpasswd
	
RUN service sshd start && service sshd stop

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
	
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]


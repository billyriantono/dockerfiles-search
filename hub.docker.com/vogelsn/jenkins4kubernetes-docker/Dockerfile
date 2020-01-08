FROM jenkins

EXPOSE 22

#install SSH Server as Root, configure it and run it
USER root
RUN apt-get update
RUN apt-get -y install openssh-server
RUN sed -i "s%PermitRootLogin without-password%PermitRootLogin yes%g" /etc/ssh/sshd_config
RUN echo "root:toor" | chpasswd
CMD \
/etc/init.d/ssh start && \
java -Dorg.apache.activemq.SERIALIZABLE_PACKAGES=* -jar monitoringserver.jar

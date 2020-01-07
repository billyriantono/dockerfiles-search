#image tomcat-alpine
FROM tomcat:alpine

# install apache
RUN apk add apache2

#install sshd 
RUN apk add openssh

#add keygen
RUN ssh-keygen -A

#Permit RootLogin yes
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config

#install supervisor use run multiple services in a container
RUN apk add supervisor
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /etc/supervisor/conf.d


EXPOSE 8080 80 22
COPY supervisor.conf /etc/supervisor.conf
CMD ["supervisord", "-c", "/etc/supervisor.conf"]

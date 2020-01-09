#FROM - Image to start building on.
FROM ubuntu

#MAINTAINER - Identifies the maintainer of the dockerfile.
MAINTAINER vjfernan@di

#RUN - Runs a command in the container.
RUN apt-get update && apt-get install -y apache2 && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

#WORKDIR - Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY and ADD 
#instructions that follow it in the Dockerfile.
WORKDIR /var/www/html

#COPY - Copies new files or directories from <src> and adds them to the filesystem 
#of the container at the path <dest>.
COPY index.html index.html

#ENV - Sets the environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

#EXPOSE - The container listens on the specified network ports at runtine.
#The EXPOSE instruction does not actually publish the port.
EXPOSE 80

#CMD - Identifies the command that should be used by default when running the image
#as a container.
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

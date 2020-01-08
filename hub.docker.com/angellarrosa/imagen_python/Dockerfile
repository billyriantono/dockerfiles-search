FROM ubuntu
RUN apt-get update
RUN apt-get install -y python
RUN apt-get install -y iputils-ping && apt-get install -y wget \
&& echo 1.0 >> /etc/version

##Workdir##
RUN mkdir /datos
WORKDIR /datos
RUN touch fichero.txt
RUN mkdir /datos1
WORKDIR /datos1
RUN touch fichero2.txt

##ENV##
ENV dir=/data dir1=/data1
RUN mkdir $dir && mkdir $dir1

##EXPOSE##
RUN apt-get install -y apache2
EXPOSE 80
ADD entrypoint.sh /datos1

##VOLUMEN##
ADD paginaweb /var/www/html
VOLUME ["/var/www/html"]

##CMD##
CMD /datos1/entrypoint.sh

##Entrypoint##
#ENTRYPOINT ["/bin/bash"]

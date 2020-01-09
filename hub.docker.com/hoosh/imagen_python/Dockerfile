FROM ubuntu
RUN apt update
RUN apt-get install -y python
RUN echo 1.0 > /etc/version && apt-get install -y git \
&& apt-get install -y iputils-ping


###WORKDIR####
WORKDIR /datos
RUN touch fi.txt
WORKDIR /datos/prueba
RUN touch hola.txt

###COPY###
#COPY maven.tar .
#COPY maven.tar /datos

###ADD###
#ADD docs docs
ADD f* /datos/

###ENV###
#ENV dir2=/data2
#RUN mkdir $dir2	
#ARG user
#ENV user_docker $user
#ADD add_user.sh /datos
#RUN /datos/add_user.sh

###EXPOSE###
RUN apt-get install -y apache2
EXPOSE 80
ADD entrypoint.sh /datos
CMD /datos/entrypoint.sh

###VOLUME###
ADD paginas /var/www/html
VOLUME ["/var/www/html"]
	
###ENTRYPOINT####
#ENTRYPOINT ["/bin/bash"]

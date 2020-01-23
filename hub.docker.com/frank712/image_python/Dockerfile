FROM ubuntu
RUN apt-get update
RUN apt-get install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git \
	&& apt-get install -y iputils-ping

##WORKDIR##
RUN mkdir /data_1
WORKDIR /data_1
RUN touch README.txt
RUN mkdir /data_2
WORKDIR /data_2
RUN touch README_2.txt

##COPY##
COPY index.html .
COPY app.log /data_1

##ADD##
ADD docs docs
ADD *txt /data_1/
ADD f.tar.gz .

##ENV##
ENV dir_0=/data_0 dir_2=/tmp_2
RUN mkdir $dir_0 && mkdir $dir_2

##ARG##
#ARG new_dir
#RUN mkdir $new_dir
#ARG user
#ENV user_docker $user
#ADD add_user.sh /data_1
#RUN /data_1/add_user.sh

##EXPOSE##
RUN apt-get install -y apache2
EXPOSE 80

##VOLUME##
ADD paginas /var/www/html
VOLUME ["/var/www/html"]

##CMD##
ADD entrypoint.sh /data_1
CMD /data_1/entrypoint.sh

##ENTRYPOINT##
#ENTRYPOINT ["/bin/bash"]


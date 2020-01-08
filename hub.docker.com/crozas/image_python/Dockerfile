FROM ubuntu
RUN apt-get update 
RUN apt-get install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git && apt-get install -y iputils-ping 


##ENV##

ENV dir=/datos1
#RUN
RUN mkdir $dir

#ARG 
#ARG dir2
#RUN mkdir $dir2
#ARG user
#ENV user_docker $user
#ADD add_user.sh .
#RUN ./add_user.sh 


##EXPOSE##
RUN apt-get install -y apache2
EXPOSE 80
ADD entrypoint.sh /datos1

##VOLUM

ADD paginas /var/www/html
VOLUME ["/var/www/html"]



##CMD
CMD /datos1/entrypoint.sh 

##ENTRY POINTo
#ENTRYPOINT ["/bin/bash"]


FROM ubuntu 
RUN apt-get update 
RUN apt-get install -y apache2 
RUN apt-get install -y apache2-bin
RUN apt-get clean 
EXPOSE 80 
EXPOSE 8080
CMD service apache2 start

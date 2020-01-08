FROM php:7.2-apache

RUN apt-get update
RUN apt-get install python3 python3-pip wget  gnupg2 -y
RUN wget https://deb.nodesource.com/setup_10.x
RUN chmod +x setup_10.x
RUN bash ./setup_10.x
RUN apt-get install nodejs curl git -y
RUN pip3 install tensorflow pillow
RUN npm install forever -g
 
CMD [ "bash" ]
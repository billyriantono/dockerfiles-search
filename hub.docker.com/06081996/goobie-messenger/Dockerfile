#Centos 7.4.1708 official image
FROM centos:7.4.1708

ENV nodeversion="10.4.1"

RUN yum install wget net-tools git -y

RUN wget https://nodejs.org/dist/v$nodeversion/node-v$nodeversion-linux-x64.tar.xz

#RUN git clone https://Lewis_Warner:Waterworld10@bitbucket.org/Lewis_Warner/goobie-messenger.git

RUN tar xf node-v*
RUN mkdir /var/www
COPY . /var/www
#RUN mv /goobie-messenger/* /var/www/
#COPY . /var/www/
#Symlinks from node to bin directory
RUN ln -s /node-v*/bin/npm /usr/bin/npm
RUN ln -s /node-v*/bin/node /usr/bin/node
RUN ln -s /node-v*/bin/npx /usr/bin/npx

RUN npm --prefix /var/www/ install /var/www/

EXPOSE 3000
#RUN > hey.txt
#ENTRYPOINT ["tail", "-f", "/hey.txt"]
ENTRYPOINT /var/www/node_modules/.bin/forever /var/www/notifications.js
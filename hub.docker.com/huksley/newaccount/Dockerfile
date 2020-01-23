FROM nginx:latest

RUN apt update
RUN apt install -y curl
RUN apt install -y git
RUN git clone https://github.com/huksley/newaccount /newaccount
RUN apt install -y npm
RUN npm install -g bower
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN cd /newaccount && bower --allow-root update
RUN rm /etc/nginx/conf.d/default.conf
COPY newaccount.conf /etc/nginx/conf.d

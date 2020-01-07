FROM yooqe/base

ENV DEBIAN_FRONTEND noninteractive

RUN wget https://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg

ADD dotdeb.list /etc/apt/sources.list.d/dotdeb.list

RUN aptitude update
RUN aptitude install -y nginx

RUN rm /etc/nginx/sites-enabled/default

ADD nginx.conf /etc/nginx/nginx.conf
ADD www.conf /etc/nginx/sites-available/www.conf
RUN ln -vs /etc/nginx/sites-available/www.conf /etc/nginx/sites-enabled/www.conf

ENTRYPOINT ["nginx"]

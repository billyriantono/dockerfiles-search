FROM base/archlinux:2018.09.01

MAINTAINER yashen@gmail.com

RUN mkdir /gooderp
WORKDIR /gooderp
RUN pacman -Sy --noconfirm gcc python2-pip libxml2 python2-lxml  nodejs-less
RUN pip2 install -r https://raw.githubusercontent.com/osbzr/base/master/requirements.txt
RUN pip2 install simplejson
RUN pip2 install -U psycopg2
RUN mkdir base addons config data log
VOLUME ["/gooderp/base","/gooderp/addons","/gooderp/config","/gooderp/data","/gooderp/log"]
ENTRYPOINT ["python2","base/odoo-bin","-c","config/gooderp.conf"]

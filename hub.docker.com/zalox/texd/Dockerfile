FROM node

RUN wget http://www.github.com/zalox/Texd/archive/master.tar.gz \
 && tar xvzf master.tar.gz \
 && rm master.tar.gz \
 && mv Texd-master /Texd \
 && cd /Texd \
 && npm install -g typescript \
 && npm install \
 && npm install -g tsd \
 && tsd install \
 && chmod -R 744 typings \
 && tsc || return 0
 
WORKDIR /Texd

EXPOSE 3000 3001

CMD ["node", "server", "--db", "mongodb"]

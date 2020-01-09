FROM node

LABEL maintainer="mynes"

RUN apt-get update

RUN apt-get install -y python3

RUN apt-get install -y python3-pip

RUN pip3 install mkdocs

RUN npm install -g typescript

RUN mkdir /notes

ADD apps /notes/apps

ADD front /notes/front

ADD src /notes/src

ADD conf.yml /notes

ADD init.sh /notes

ADD package.json /notes

ADD tsconfig.json /notes

RUN chmod +x /notes/init.sh

WORKDIR /notes

RUN cd /notes && npm install

RUN cd /notes && tsc

ENTRYPOINT /notes/init.sh
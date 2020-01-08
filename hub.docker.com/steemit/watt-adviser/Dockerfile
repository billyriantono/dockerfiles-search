FROM node:8

WORKDIR /var/app
RUN mkdir -p /var/app
COPY . /var/app



RUN apt-get update && apt-get install bash jq moreutils zip git python-pip python-dev build-essential supervisor zip -y

RUN pip install --upgrade pip
RUN pip install --upgrade awscli

RUN curl -sSL https://get.docker.com/ | sh

RUN which docker

ADD ./build.sh /var/app/build.sh
RUN chmod +x /var/app/build.sh

ADD ./libs/trycatch.sh /var/app/trycatch.sh
RUN chmod +x /var/app/trycatch.sh

VOLUME ["/var/run/docker.sock"]

CMD ["bash","/var/app/build.sh"]

FROM docker
MAINTAINER jeanvincent45@gmail.com

RUN apk --no-cache add --update curl python python-dev py-pip
RUN pip install awscli ecs-deploy --upgrade --user
RUN export PATH=~/.local/bin:/usr/bin/:$PATH

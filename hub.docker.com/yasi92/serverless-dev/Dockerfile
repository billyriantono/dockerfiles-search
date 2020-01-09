FROM node:6.10
LABEL maintainer="Yasiru Nilan <nilanyasiru@gmail.com>"

RUN apt-get update -y && \
    apt-get install awscli -y && \
    apt-get clean
RUN npm install -g serverless

# expose ports
EXPOSE 8089

WORKDIR /home/svless
CMD ["sls", "--help"]
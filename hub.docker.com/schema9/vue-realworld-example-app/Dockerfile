FROM ubuntu:latest

MAINTAINER schema9@gmail.com

RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y yarn
RUN apt-get install -y npm

CMD ["mkdir", "git"]
CMD ["cd", "git"]
CMD ["git", "clone", "https://github.com/kimhaegyeong/vue-realworld-example-app"]
CMD ["npm", "install", "-g", "vue-cli"]
CMD ["cd", "vue-realworld-example-app"]
CMD ["npm", "run", "dev"]

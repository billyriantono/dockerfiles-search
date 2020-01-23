FROM node:latest

RUN apt-get update -qq
RUN apt-get install -y build-essential ruby ruby-dev
RUN gem install sass
RUN gem install compass
RUN npm install gulp-cli grunt-cli jspm -g

COPY version.sh /bin/versions
RUN chmod +x /bin/versions

RUN useradd dev
ENV HOME /home/dev

RUN mkdir /src
WORKDIR /src

USER dev

CMD ["bash"]

# the base image includes java 8, nodejs 10.16.0, python 3.7.3, pip and pipenv
FROM python:3.7.3
RUN apt-get update \
  && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  && apt-get install -y nodejs

RUN apt-get install -y openjdk-8-jdk

RUN java -version
RUN python --version
RUN node --version

RUN npm install -g yarn
RUN npm install -g pm2
WORKDIR /usr/src/app
RUN git clone https://github.com/tetrascience/ts-tool-wait-for-them.git /usr/src/lib/wait/
RUN chmod +x /usr/src/lib/wait/wait-for-it.sh
RUN chmod +x /usr/src/lib/wait/wait-for-them.sh
RUN python --version
RUN pip install pipenv
RUN pipenv --support
RUN java -version
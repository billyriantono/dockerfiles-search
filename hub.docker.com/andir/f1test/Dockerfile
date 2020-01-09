FROM python:3.7
RUN pip install --upgrade pip
RUN apt-get update && apt-get install -y nodejs npm gettext
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN npm install -g node-sass
RUN apt-get autoremove -y
RUN apt-get clean

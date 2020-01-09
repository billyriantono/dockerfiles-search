FROM node:8
RUN mkdir /code
COPY . /code/
WORKDIR /code/
RUN npm install express
RUN npm run build
RUN npm install serve
ENV NODE_PATH=/code/node_modules
ENV PATH=$PATH:/code/node_modules/.bin
#RUN apt update
#RUN apt install python3-pip -y
#RUN pip3 install requirements.txt

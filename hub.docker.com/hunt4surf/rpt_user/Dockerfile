FROM node:latest 
RUN mkdir -p /rpt_user
WORKDIR /rpt_user
COPY package.json /rpt_user
RUN npm install
COPY . /rpt_user
RUN sed -i 's/\r$//' /rpt_user/wait-for-it.sh  && chmod +x /rpt_user/wait-for-it.sh

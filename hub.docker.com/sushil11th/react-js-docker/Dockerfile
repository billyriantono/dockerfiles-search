FROM node
LABEL company="FIRMINIQ"
LABEL author="Sushil"
LABEL version="1.0.0"
#Install AWS CLI
RUN apt-get update
RUN apt-get install -y python-pip
RUN pip install awscli
RUN mkdir -p /root/.aws
COPY .aws/ /root/.aws
RUN mkdir /home/frontend-ui
COPY Frontend-UI/ /home/frontend-ui/
#COPY nodeconf/ /home/frontend-ui/
WORKDIR /home/frontend-ui/
RUN npm install && npm install -g pm2
RUN npm run build
WORKDIR /home/frontend-ui/build
#S3 Deploy
RUN aws s3 cp ./ s3://ks8-reactapp --recursive

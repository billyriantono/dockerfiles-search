FROM ubuntu:18.04

RUN apt update -y && apt upgrade -y
RUN apt install -y python3.7 python3-pip nodejs npm libssl1.0-dev libffi-dev
RUN pip3 install --upgrade pip
RUN npm install -g serverless

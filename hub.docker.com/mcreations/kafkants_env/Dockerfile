FROM python:3.7

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y build-essential nodejs jq

RUN npm install -g serverless
RUN pip install pipenv

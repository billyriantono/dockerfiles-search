FROM node:6.9.5

RUN apt-get update && apt-get install -y\
      python \
      python-pip \
      libpython-dev \
      unzip

RUN pip install \
      awsebcli==3.7.4 \
      awscli==1.11.52

RUN npm install -g yarn@0.19.1 codeclimate-test-reporter@0.4.1

CMD ["node"]

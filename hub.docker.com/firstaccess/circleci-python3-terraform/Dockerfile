FROM circleci/python:3

RUN sudo apt-get install --assume-yes apt-utils jq

USER circleci

WORKDIR /home/circleci

RUN sudo apt-get install --assume-yes jq

RUN curl -o terraform.zip $(curl https://releases.hashicorp.com/index.json | jq '{terraform}' | egrep "linux.*amd64" | sort --version-sort -r | head -1 | awk -F[\"] '{print $4}')

RUN unzip terraform.zip

RUN sudo mv terraform /usr/local/bin
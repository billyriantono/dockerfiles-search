FROM circleci/node:10
ENV PATH="${PATH}:~/.local/bin/"
RUN sudo apt-get -y install python-pip && \
pip install awscli && \
sudo npm i -g cfn-create-or-update


# This docker image relies upon circleci's node image and has aws cli preinstalled
# You can publish or update this in docker hub if needed
# 
# docker build -t yourdockerhubusername/repositoryname .
# docker login
# docker push yourdockerhubusername/repositoryname
FROM circleci/node:8.10.0
RUN sudo apt-get -y -qq install python3.4-dev \
    && sudo curl -O https://bootstrap.pypa.io/get-pip.py \
    && sudo python3.4 get-pip.py \
    && sudo pip install awscli --upgrade

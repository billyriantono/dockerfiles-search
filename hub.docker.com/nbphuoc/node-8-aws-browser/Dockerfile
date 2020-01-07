FROM circleci/node:8.2-browsers

RUN sudo apt-get update && sudo apt-get install -y \
    php5-mcrypt \
    python-pip \
    python-dev

RUN pip install awscli awsebcli --upgrade --user
RUN echo PATH="~/.local/bin:${PATH}" >> ~/.bashrc
ENV PATH="~/.local/bin:${PATH}"

##################################### Install heroku ################################
RUN sudo wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh

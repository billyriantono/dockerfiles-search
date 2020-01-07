FROM circleci/node:10.9

# Add Mongo Repo
RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
RUN echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list

# Install http apt transport (for yarn)
RUN sudo apt-get update \
  && sudo apt-get install -qqy apt-transport-https \
  && sudo apt-get install lsb-release \
  && sudo apt-get install mongodb-org-shell \
  && sudo apt-get install mongodb-org-tools

# Install gcloud
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - && \
    sudo apt-get update -y && sudo apt-get install google-cloud-sdk -y
    
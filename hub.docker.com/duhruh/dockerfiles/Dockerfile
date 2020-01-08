FROM ruby:2.4

RUN apt-get update -y && apt-get install wget unzip -y
RUN wget https://releases.hashicorp.com/packer/1.2.1/packer_1.2.1_linux_arm64.zip
RUN unzip packer_1.2.1_linux_arm64.zip
RUN mv packer /bin/packer
RUN chmod +x /bin/packer

RUN gem install berkshelf

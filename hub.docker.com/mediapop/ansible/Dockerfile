FROM circleci/python:3.6.4-stretch

RUN sudo pip install "ansible" --upgrade

RUN wget -P /tmp https://github.com/adammck/terraform-inventory/releases/download/v0.6.1/terraform-inventory_v0.6.1_linux_amd64.zip &&\
    sudo unzip /tmp/terraform-inventory_v0.6.1_linux_amd64.zip -d /usr/local/bin &&\
    rm /tmp/terraform-inventory_v0.6.1_linux_amd64.zip

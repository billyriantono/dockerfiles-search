FROM circleci/openjdk:8-jdk

WORKDIR /tmp

# Installation Instructions from SF https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm#sfdx_setup_install_cli
RUN wget https://developer.salesforce.com/media/salesforce-cli/sfdx-v5.99.1-d7efd75-linux-amd64.tar.xz
RUN tar -xvJf sfdx-v5.99.1-d7efd75-linux-amd64.tar.xz
RUN sfdx/install


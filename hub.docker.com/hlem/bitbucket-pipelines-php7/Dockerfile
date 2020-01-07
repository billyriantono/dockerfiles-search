FROM edbizarro/bitbucket-pipelines-php7

RUN sudo apt-get update \
 && sudo apt-get install make \
 && sudo apt-get autoclean -y \
 && sudo apt-get --purge autoremove -y \
 && sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


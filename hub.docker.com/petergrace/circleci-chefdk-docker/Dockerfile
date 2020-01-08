FROM circleci/ruby:2.4-jessie-node-browsers

RUN sudo wget https://packages.chef.io/files/stable/chefdk/3.0.36/debian/8/chefdk_3.0.36-1_amd64.deb \
 && sudo dpkg -i chefdk*.deb \
 && sudo rm -f chefdk*.deb


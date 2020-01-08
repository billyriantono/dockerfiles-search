# https://github.com/sjitech/ubuntu-with-utils/blob/master/Dockerfile
FROM osexp2000/ubuntu-with-utils

USER root

RUN wget https://packages.chef.io/files/stable/chefdk/2.4.17/ubuntu/16.04/chefdk_2.4.17-1_amd64.deb && \
    dpkg -i chefdk_2.4.17-1_amd64.deb && \
    rm chefdk_2.4.17-1_amd64.deb

ENV PATH="$PATH:/opt/chefdk/embedded/bin"

USER devuser

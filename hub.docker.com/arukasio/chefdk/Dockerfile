FROM circleci/ruby
LABEL maintainer="support@arukas.io"

ENV CHEFDK_VERSION 4.5.0

ADD https://packages.chef.io/files/stable/chefdk/${CHEFDK_VERSION}/debian/9/chefdk_${CHEFDK_VERSION}-1_amd64.deb /tmp/chefdk_${CHEFDK_VERSION}.deb
RUN sudo dpkg -i /tmp/chefdk_${CHEFDK_VERSION}.deb && \
    sudo rm -rf /tmp/chefdk_${CHEFDK_VERSION}.deb

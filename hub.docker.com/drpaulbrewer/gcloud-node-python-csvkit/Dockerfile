FROM google/cloud-sdk
MAINTAINER drpaulbrewer@eaftc.com
# see https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions
RUN apt-get update && apt-get install -y apt-utils && apt-get install -y git p7zip-full && apt-get upgrade -y
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs
RUN pip install csvkit
RUN useradd -m work
USER work
WORKDIR /home/work

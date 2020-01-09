FROM ubuntu:18.04

# initial setup
RUN apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y apt-utils wget curl build-essential gcc g++ make

# install miniconda
RUN wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh \
	&& bash ~/miniconda.sh -b -p $HOME/miniconda
ENV PATH="/root/miniconda/bin:$PATH"

# install node & npm
RUN wget https://deb.nodesource.com/setup_8.x \
	&& bash setup_8.x \
	&& rm setup_8.x \
 	&& apt-get install -y nodejs

# install yarn
RUN curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
	&& echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
	&& apt-get update \
	&& apt-get install -y yarn


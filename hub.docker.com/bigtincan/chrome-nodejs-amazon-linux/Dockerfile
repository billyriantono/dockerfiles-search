FROM "amazonlinux"

RUN yum update -y && yum install -y gcc-c++ make \ 
    && curl https://intoli.com/install-google-chrome.sh | bash - \
	&& curl -sL https://rpm.nodesource.com/setup_13.x | bash - \
	&& curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo \
	&& yum update -y && yum install -y nodejs npm yarn

ENV NODE_OPTIONS=--max_old_space_size=8000
RUN useradd -ms /bin/bash chrome
RUN usermod -aG audio,video chrome

RUN mkdir -p /home/chrome && chown -R chrome:chrome /home/chrome 

USER chrome

WORKDIR /home/chrome

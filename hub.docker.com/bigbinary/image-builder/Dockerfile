FROM circleci/ubuntu-server:trusty-latest

ENV VERBOSE true

# Avoid any installation scripts interact with upstart
# So divert now, but undivert at the end
# You shouldn't change the line unless you understand the consequence
RUN echo 'exit 101' > /usr/sbin/policy-rc.d \
	&& chmod +x /usr/sbin/policy-rc.d \
        && dpkg-divert --local --rename --add /sbin/initctl \
        && ln -s /bin/true /sbin/initctl

ADD circleci-install /usr/local/bin/circleci-install
ADD circleci-provision-scripts/base.sh circleci-provision-scripts/circleci-specific.sh /opt/circleci-provision-scripts/
RUN circleci-install base_requirements && circleci-install circleci_specific

# Installing java early beacuse a few things have the dependency to java (i.g. cassandra)
ADD circleci-provision-scripts/java.sh /opt/circleci-provision-scripts/java.sh
RUN circleci-install java oraclejdk8 && circleci-install java openjdk8

ADD circleci-provision-scripts/misc.sh /opt/circleci-provision-scripts/misc.sh
RUN for package in sysadmin devtools jq; do circleci-install $package; done

# Browsers
ADD circleci-provision-scripts/firefox.sh circleci-provision-scripts/chrome.sh circleci-provision-scripts/phantomjs.sh /opt/circleci-provision-scripts/
RUN circleci-install firefox_version 46.0.1
RUN circleci-install chrome_latest
RUN circleci-install phantomjs

# Qt
ADD circleci-provision-scripts/qt.sh /opt/circleci-provision-scripts/qt.sh
RUN circleci-install qt

# Install deployment tools
ADD circleci-provision-scripts/awscli.sh circleci-provision-scripts/gcloud.sh circleci-provision-scripts/heroku.sh /opt/circleci-provision-scripts/
RUN for package in awscli gcloud heroku; do circleci-install $package; done

# Languages
ARG use_precompile=true
ENV USE_PRECOMPILE=$use_precompile RUN_APT_UPDATE=true
RUN curl -s https://packagecloud.io/install/repositories/circleci/trusty/script.deb.sh | sudo bash
ADD circleci-provision-scripts/python.sh /opt/circleci-provision-scripts/python.sh
RUN circleci-install python 2.7.11
RUN circleci-install python pypy-4.0.1
RUN sudo -H -i -u ubuntu pyenv global 2.7.11

ADD circleci-provision-scripts/nodejs.sh /opt/circleci-provision-scripts/nodejs.sh
RUN circleci-install nodejs 6.1.0
RUN sudo -H -i -u ubuntu nvm alias default 4.2.6

ADD circleci-provision-scripts/ruby.sh /opt/circleci-provision-scripts/ruby.sh
RUN circleci-install ruby 2.3.1
RUN sudo -H -i -u ubuntu rvm use 2.3.1 --default


# Docker have be last - to utilize cache better
ADD circleci-provision-scripts/docker.sh /opt/circleci-provision-scripts/docker.sh
RUN circleci-install docker && circleci-install docker_compose

# When running in unprivileged containers, need to use CircleCI Docker fork
ARG TARGET_UNPRIVILEGED_LXC
RUN if [ "$TARGET_UNPRIVILEGED_LXC" = "true" ]; then circleci-install circleci_docker; fi

# Undivert upstart
# You shouldn't change the line unless you understad the consequence
RUN rm /usr/sbin/policy-rc.d && rm /sbin/initctl && dpkg-divert --rename --remove /sbin/initctl

# Add rest of provisioning files -- add at end to avoid cache invalidation
ADD circleci-provision-scripts /opt/circleci-provision-scripts

# We need Dockerfile because unit test parses Dockerfile to make sure all versions are installed
ADD Dockerfile /opt/circleci/Dockerfile

# ****Custom Install packages***
RUN sudo -H -i -u ubuntu pip install --upgrade pip
RUN sudo -H -i -u ubuntu pip install simplejson==3.8.1 requests==2.6.0 robotframework==2.9.2 robotframework-selenium2library==1.7.4 robotframework-pabot==0.20 robotframework-selenium2screenshots==0.7.2

ARG IMAGE_TAG
RUN echo $IMAGE_TAG > /opt/circleci/image_version

ADD pkg-versions.sh /opt/circleci/bin/pkg-versions.sh

LABEL circleci.user="ubuntu"

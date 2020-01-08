FROM circleci/android:api-28-alpha

USER root

RUN apt-get install -y ruby && gem install fastlane -NV
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
RUN apt-get install git-lfs
RUN apt-get install jq

USER circleci


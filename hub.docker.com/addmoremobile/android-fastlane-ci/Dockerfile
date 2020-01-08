FROM jangrewe/gitlab-ci-android:latest
SHELL ["/bin/bash", "-c"]

RUN apt-get -qq update && \
    apt-get install -qqy \
      ruby-full \
      build-essential \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN gem install fastlane

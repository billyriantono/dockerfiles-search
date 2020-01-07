FROM ubuntu:16.10

# Install curl, bzip2, git, libfontconfig (an undocumented dependency of phantomjs) and build-tools
RUN apt-get update && \
    apt-get install -y curl bzip2 git libfontconfig && \
    apt-get install -y bcrypt make python g++ && \
    rm -rf /var/lib/apt/lists/*

# Add a user and a group called meteor
RUN groupadd meteor && adduser --ingroup meteor --disabled-password --gecos "" --home /home/meteor meteor

USER meteor
ENV METEOR_RELEASE 1.6
RUN curl  https://install.meteor.com/ 2>/dev/null | sed 's/^RELEASE/#RELEASE/'| RELEASE=$METEOR_RELEASE sh

# Linking meteor
USER root
RUN ln -s /home/meteor/.meteor/meteor /usr/local/bin/

# Set locale (needed to start MongoDB)
RUN locale-gen en_US.UTF-8
RUN export LC_ALL=en_US.UTF-8

USER meteor

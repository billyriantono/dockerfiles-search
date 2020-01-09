FROM khornberg/aws-codebuild-node

# Install latest, packages then clean up!
# https://github.com/cypress-io/cypress-docker-images/blob/master/base/centos7/Dockerfile

RUN yum update -y && \
    yum install -y \
    alsa-lib* \
    GConf2* \
    gtk2-2.24* \
    libXScrnSaver* \
    libXtst* \
    xorg-x11-server-Xvfb && \
    npm install -g yarn && \
    yarn global add cypress --cache-folder ./ycache && \
    npm cache clear --global --force && \
    yum clean all && \
    rm -rf ./ycache /tmp /var/cache/yum /var/tmp

# This is a build-only image, so no CMD.

FROM fgrehm/devstep:v0.3.0

USER root


RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get -y install nodejs-legacy npm && \
    apt-get clean && \
    npm install -g yo gulp bower && \
    npm install -g generator-gulp-angular

RUN mkdir -p /workspace && chown developer /workspace

RUN chown developer /home/devstep/tmp

USER developer

WORKDIR /workspace

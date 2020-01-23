FROM strongloop/strong-pm

USER root
RUN npm install --global \
    strongloop \
    # yarn \
    && npm cache clear \
    && sl-pm-install

WORKDIR /usr/app

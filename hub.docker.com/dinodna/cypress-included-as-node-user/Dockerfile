# direct copy of the following, but as user node
# https://github.com/cypress-io/cypress-docker-images/blob/master/included/3.7.0/Dockerfile
FROM cypress/browsers:node12.6.0-chrome77

# BEGIN_DIFF
RUN \
  mkdir /test_as_node_user && \
  chown -R node /test_as_node_user && \
  chown -R node /usr/local
WORKDIR /test_as_node_user
USER node
# END_DIFF

# avoid too many progress messages
# https://github.com/cypress-io/cypress/issues/1243
ENV CI=1
ARG CYPRESS_VERSION="3.7.0"

RUN echo "whoami: $(whoami)"
RUN npm config -g set user $(whoami)
RUN npm install -g "cypress@${CYPRESS_VERSION}"
RUN cypress verify

# Cypress cache and installed version
RUN cypress cache path
RUN cypress cache list

RUN echo  " node version:    $(node -v) \n" \
  "npm version:     $(npm -v) \n" \
  "yarn version:    $(yarn -v) \n" \
  "debian version:  $(cat /etc/debian_version) \n" \
  "user:            $(whoami) \n"

ENTRYPOINT ["cypress", "run"]

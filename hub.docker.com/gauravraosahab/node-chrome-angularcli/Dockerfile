# Getting node image with chrome
# Node - 10.7.0
# Chrome Version - 67.0.3396 (2018-05-29)
FROM gauravraosahab/docker_node_chrome:1.0.3

# Install AngularCli@1.7.4
RUN npm config set depth 0 \
  && npm cache clean --force \
  && npm i -g @angular/cli@6.0.8 --unsafe

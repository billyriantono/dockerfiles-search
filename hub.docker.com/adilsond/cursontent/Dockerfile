FROM screwdrivercd/screwdriver:v0.5.800

RUN mkdir -p /opt/files
COPY files/* /opt/files/

RUN cd /usr/src/app && npm install screwdriver-scm-bitbucket@3.4.9

# NOTE: in order to support custom hostNetwork and privilege mode for specific containers
#       will will add the handlebar helps and inject some code into the k8s executor
RUN cd /usr/src/app && npm install handlebars-helpers
RUN cp -f /opt/files/pod.yaml.hbs /usr/src/app/node_modules/screwdriver-executor-k8s/config/pod.yaml.hbs
RUN sed -i "s/const handlebars = require('handlebars');/const handlebars = require('handlebars');\nconst helpers = require('handlebars-helpers')();/" /usr/src/app/node_modules/screwdriver-executor-k8s/index.js

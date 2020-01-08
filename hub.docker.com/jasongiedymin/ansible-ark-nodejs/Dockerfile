#
# jasongiedymin/ansible-ark-nodejs
#   docker build -t jasongiedymin/ansible-ark-nodejs .
#
# Requires:
# jasongiedymin/ansible-nodejs
#   https://github.com/AnsibleShipyard/ansible-nodejs
#

FROM jasongiedymin/ansible-nodejs
MAINTAINER AnsibleShipyard

# Working dir
ENV WORKDIR /tmp/build/ansible-ark-nodejs
ENV NODE_ENV production

# ADD
ADD tasks $WORKDIR/tasks
ADD tests $WORKDIR/tests
ADD vars $WORKDIR/vars
ADD templates $WORKDIR/templates
ADD handlers $WORKDIR/handlers

# Here we continue to use add because
# there are a limited number of RUNs
# allowed.
ADD tests/inventory /etc/ansible/hosts
ADD tests/playbook.yml $WORKDIR/playbook.yml

# Execute
RUN ansible-playbook $WORKDIR/playbook.yml -c local -vvvv

# TODO: in debug mode, leave. Prod, cleanup
# Cleanup
# RUN rm -R $WORKDIR

EXPOSE 2368

# By default the playbook uses an init.d but since docker doesn't
# the default will be safely ignored. Instead we rely on the
# docker CMD
CMD ["node", "/nodejs-apps/nodejs_app.js"]

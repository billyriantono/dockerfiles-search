FROM node:8-slim

ENV CI_PROJECT_DIR=/home/node/

RUN npm install --loglevel warn -g \
    #
    # eslint
    eslint@^5.16.0 \
    eslint-config-standard@^12.0.0 \
    eslint-plugin-promise@^4.2.1 \
    eslint-plugin-standard@^4.0.0 \
    eslint-plugin-import@^2.17.3 \
    eslint-plugin-node@^9.1.0 \
    eslint-plugin-compat@^3.2.0 \
    #
    # Stylelint
    stylelint@^10.0.0 \
    stylelint-config-standard@^18.3.0 \
    > /dev/null

WORKDIR /home/node

COPY ./bin/ /opt/docker/bin/

RUN chmod +x /opt/docker/bin/*.sh

CMD ["/bin/bash"]

USER root

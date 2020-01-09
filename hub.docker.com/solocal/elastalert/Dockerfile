FROM bitsensor/elastalert:2.0.1

# Set permission as unpriviledge user, compatible with Kubernetes
RUN mkdir -p /opt/elastalert/rules/ /opt/elastalert/server_data/tests/ && chown -R node:node /opt

USER node

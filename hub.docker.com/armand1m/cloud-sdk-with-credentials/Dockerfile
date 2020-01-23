FROM google/cloud-sdk:alpine

COPY entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]

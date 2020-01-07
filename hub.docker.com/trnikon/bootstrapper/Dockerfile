FROM offlinegmbh/oc-bootstrapper:develop

RUN mkdir /root/.ssh/
RUN mkdir /temp

COPY docker-entrypoint.sh /bin/docker-entrypoint.sh
RUN chmod +x /bin/docker-entrypoint.sh
ENTRYPOINT ["/bin/docker-entrypoint.sh"]

WORKDIR /build
CMD ["/tmp/bootstrapper/october"]
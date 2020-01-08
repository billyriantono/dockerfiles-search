FROM kibana:6.6.1

# https://docs.search-guard.com/latest/search-guard-versions
ENV SEARCH_GUARD_KIBANA_MAJOR "6"
ENV SEARCH_GUARD_KIBANA_VERSION "6.6.1-18.1"
ENV SEARCH_GUARD_KIBANA_ZIP "/tmp/search-guard-kibana-plugin-${SEARCH_GUARD_KIBANA_VERSION}.zip"

RUN curl -o "${SEARCH_GUARD_KIBANA_ZIP}" \
    "https://oss.sonatype.org/service/local/repositories/releases/content/com/floragunn/search-guard-kibana-plugin/${SEARCH_GUARD_KIBANA_VERSION}/search-guard-kibana-plugin-${SEARCH_GUARD_KIBANA_VERSION}.zip"
RUN bin/kibana-plugin install "file://${SEARCH_GUARD_KIBANA_ZIP}"

#COPY entrypoint.sh /entrypoint.sh
#RUN chmod u+x /entrypoint.sh

#CMD ["/entrypoint.sh"]

FROM plone
MAINTAINER "Manuel Oliver" http://www.uclv.edu.cu

VOLUME /data

COPY docker-entrypoint.sh /

EXPOSE 8080
USER plone
WORKDIR /plone/instance

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["start"]

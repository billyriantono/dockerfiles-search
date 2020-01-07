FROM vituity/s2i-java

USER 0
RUN yum install -y libreoffice && yum clean all
RUN chown -R jboss:root /deployments \
    && chmod -R "g+rwX" /opt/jboss \
    && chown -R jboss:root /opt/jboss \
    && chmod 664 /etc/passwd
COPY run /usr/local/s2i/run
RUN chmod 755 /usr/local/s2i/run
USER 1000

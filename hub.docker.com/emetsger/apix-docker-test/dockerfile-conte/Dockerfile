FROM atlassian/confluence-server

ENV CONF_INSTALL  /opt/atlassian/confluence

RUN set -x \
    && curl -Ls  "https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.44.tar.gz" | tar -xz --directory "${CONF_INSTALL}/confluence/WEB-INF/lib" --strip-components=1 --no-same-owner "mysql-connector-java-5.1.44/mysql-connector-java-5.1.44-bin.jar"
    

#Build mhsendmail
FROM docksal/cli:2.2-php7.2
RUN curl -fsSL https://raw.githubusercontent.com/andock-ci/pipeline/master/install-pipeline | sh
COPY startup.sh /opt/startup.sh
ENTRYPOINT ["/opt/startup.sh"]
RUN ["chmod", "+x", "/opt/startup.sh"]
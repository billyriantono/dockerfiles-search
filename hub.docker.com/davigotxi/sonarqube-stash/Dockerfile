## This is the 6.7 LTS version
# https://github.com/SonarSource/docker-sonarqube/blob/abaf14c38297974eb5de295d42e83066ddb84751/6.7.7-community/Dockerfile
FROM sonarqube:6.7-community

USER root
COPY --chown=sonarqube:sonarqube plugins/* /opt/sonarqube/extensions/plugins/
USER sonarqube

ENTRYPOINT ["./bin/run.sh"]

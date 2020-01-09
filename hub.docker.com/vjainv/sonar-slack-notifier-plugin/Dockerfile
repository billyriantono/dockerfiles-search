FROM sonarqube:latest
RUN cd /opt/sonarqube/extensions/plugins/

USER root
RUN apt-get install wget
RUN wget https://github.com/kogitant/sonar-slack-notifier-plugin/releases/download/2.1.2/cks-slack-notifier-2.1.2.jar
RUN pwd
RUN ls
RUN mv cks-slack-notifier-2.1.2.jar /opt/sonarqube/extensions/plugins/
RUN cd /opt/sonarqube/extensions/plugins/
RUN ls

USER sonarqube
ENTRYPOINT ["./bin/run.sh"]

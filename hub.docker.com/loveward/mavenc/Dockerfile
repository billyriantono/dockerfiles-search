FROM maven:3.6.3-jdk-13
COPY settings.xml /usr/share/maven/ref/settings-docker.xml
CMD ["/bin/bash"]
ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
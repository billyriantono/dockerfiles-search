FROM debian:jessie

# Create the jenkins user
RUN useradd -d "/var/jenkins_home" -u 1000 -m -s /bin/bash jenkins

VOLUME ["/var/jenkins_home"]

USER jenkins
CMD ["echo", "Data container for Jenkins"]
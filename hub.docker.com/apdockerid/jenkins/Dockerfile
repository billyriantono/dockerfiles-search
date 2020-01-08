FROM apdockerid/python:release
LABEL maintainer="Andreas Pettersson"
# Install software that Jenkins is depended on
RUN apt-get update && apt-get install -y \
    openjdk-8-jre \
    wget \
    gnupg2 \
    dialog \
    apt-utils \
    && rm -rf /var/lib/apt/lists/*

# Add Jenkins repository to  apt list of sources
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

# Install Jenkins
RUN apt-get update && apt-get install -y \
    jenkins \
    && rm -rf /var/lib/apt/lists/*

# Prepare Entrypoint
ENV SCRIPTS=/home/scripts
RUN mkdir -p $SCRIPTS
COPY /scripts/service_jenkins_start.py $SCRIPTS
RUN chmod +x $SCRIPTS/service_jenkins_start.py
ENTRYPOINT ["python3", "/home/scripts/service_jenkins_start.py"]

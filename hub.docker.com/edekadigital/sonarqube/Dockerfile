FROM sonarqube:7.6-community

MAINTAINER EDEKA DIGITAL GmbH <dpp@edeka.de>

ENV SONAR_STASH_REPO_URL=https://github.com/edekadigital/sonar-stash
ENV SONAR_STASH_RELEASE_FILE=sonar-stash-plugin-1.7.0-SNAPSHOT.jar
ENV SONAR_STASH_RELEASE_TAG=untagged-893829aa306f1a0827e9
ENV SONAR_PLUGINS_DIR=/opt/sonarqube/extensions/plugins

# Create Plugins directory and download the release from github
RUN mkdir -p ${SONAR_PLUGINS_DIR} && \
    cd ${SONAR_PLUGINS_DIR} && \
    wget ${SONAR_STASH_REPO_URL}/releases/download/${SONAR_STASH_RELEASE_TAG}/${SONAR_STASH_RELEASE_FILE}

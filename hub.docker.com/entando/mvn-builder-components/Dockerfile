FROM  entando/centos-base:master
LABEL MAINTAINER="Pietrangelo Masala <p.masala@entando.com>"

ENV PROJECT_HOME /home/entando

# Define path to copy artifacts from image to image
ENV COPY_ARTIFACT /home/entando/.m2/
ENV DEST_ARTIFACT /home/entando/.m2/

#The name of the artifactID to be generated
ARG PROJECT_NAME=entando-components

# The github project and branch to build from
ENV GIT_PROJECT https://github.com/entando/${PROJECT_NAME}.git
ARG BRANCH_TO_BUILD=master

# Copy artifacts from entando/mvn-builder-core image
COPY --from=entando/mvn-builder-core:master ${COPY_ARTIFACT} ${DEST_ARTIFACT}

RUN chown -R entando:entando ${DEST_ARTIFACT}

USER entando

WORKDIR ${PROJECT_HOME}

RUN git clone ${GIT_PROJECT} --branch ${BRANCH_TO_BUILD} \
&& cd ${PROJECT_NAME} \
&& mvn clean install -DskipTests && mvn clean
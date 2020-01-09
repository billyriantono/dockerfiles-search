## Build plugin
FROM gradle:5.1 AS BUILD_IMAGE

# copy artifacts
COPY --chown=gradle:gradle . /home/gradle

# gradle build
RUN gradle build --info

FROM openjdk:13-alpine

LABEL maintainer="Ismael Queiroz <ismaelqueiroz@gmail.com>"

## Default to TimeZone
ENV TZ America/Sao_Paulo

## Default to UTF-8 file.encoding
ENV LANG C.UTF-8

## Allure Versrion
ARG ALLURE_REPORT_VERSION="2.9.0"

## Allure Versrion
ENV ALLURE_REPORT_HOME=/opt/allure

## Export alure commandline
ENV PATH $PATH:$ALLURE_REPORT_HOME/bin

# Adding allure user, group, install dependencies and chage permissions
RUN set -x && apk add --update --no-cache curl grep sed unzip bash && \
    curl --insecure -o /tmp/allure-${ALLURE_REPORT_VERSION}.zip -L https://dl.bintray.com/qameta/maven/io/qameta/allure/allure-commandline/${ALLURE_REPORT_VERSION}/allure-commandline-${ALLURE_REPORT_VERSION}.zip && \
	unzip /tmp/allure-${ALLURE_REPORT_VERSION}.zip -d /opt && \
	mv /opt/allure-${ALLURE_REPORT_VERSION} /opt/allure && \
	rm /tmp/allure-${ALLURE_REPORT_VERSION}.zip

# copy artifacts
COPY --from=BUILD_IMAGE /home/gradle/allure.yml /opt/allure/config
COPY --from=BUILD_IMAGE /home/gradle/build/distributions/ci-plugin-2.9.0.zip /tmp

RUN unzip /tmp/ci-plugin-2.9.0.zip -d /opt/allure/plugins && \
    mv /opt/allure/plugins/ci-plugin-2.9.0 /opt/allure/plugins/ci-plugin && \
    rm /tmp/ci-plugin-2.9.0.zip

# Use bash if you want to run the environment from inside the shell, otherwise use the command that actually runs the underlying stuff
CMD ["allure"]
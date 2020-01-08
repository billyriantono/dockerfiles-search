FROM itminds/pipeline-tools AS pipeline-tools
FROM microsoft/dotnet:2.1-sdk-alpine

ENV DOTNET_TOOLS_HOME /root/.dotnet/tools
ENV SONAR_SCANNER_MSBUILD_VERSION 4.3.1
# embedded in the sonar-scanner-msbulid version, so check SONAR_SCANNER_HOME directory for the version
ENV EMBEDDED_SONAR_SCANNER_VERSION 3.2.0.1227
ENV SONAR_SCANNER_HOME ${DOTNET_TOOLS_HOME}/.store/dotnet-sonarscanner/${SONAR_SCANNER_MSBUILD_VERSION}/dotnet-sonarscanner/${SONAR_SCANNER_MSBUILD_VERSION}/tools/netcoreapp2.1/any
ENV MINICOVER_HOME /opt/minicover
ENV TOOLS_HOME /opt/tools
ENV JAVA_HOME=/opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin
# https://github.com/dotnet/dotnet-docker/issues/615
ENV PATH ${PATH}:${DOTNET_TOOLS_HOME}

# Install curl and nodejs + nodejs-npm
# Install glibc-2.21 which is a hard dependency of Node and Java 8. and see https://github.com/mesosphere/kubernetes-mesos/issues/801
RUN apk add --no-cache curl ca-certificates tar nodejs nodejs-npm \
	&& curl -Ls https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.21-r2/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk \
	&& apk add --allow-untrusted /tmp/glibc-2.21-r2.apk

WORKDIR /root

# Install other dependencies
RUN apk add --no-cache wget unzip jq gnupg bash git
#RUN npm i -g npm@6 currently this fails with error [Cannot find module 'npmlog']
RUN curl https://registry.npmjs.org/npm/-/npm-6.1.0.tgz -o "npm.tgz" && \
	tar xzf npm.tgz && \
	cd package && \
	node bin/npm-cli.js install -gf --prefix=/usr/local ../npm.tgz && \
	cd .. && rm npm.tgz && rm package -r

# Install Java
# Download the Oracle JRE using tricks from this repo: https://github.com/LennonRuangjaroon/alpine-java8-jdk/blob/master/Dockerfile
ARG JAVA_VERSION_MAJOR=8
ARG JAVA_VERSION_MINOR=172
ARG JAVA_VERSION_BUILD=11
ARG JAVA_PACKAGE=jdk
ARG JAVA_URL_ELEMENT=a58eab1ec242421181065cdc37240b08
RUN mkdir -p /opt &&\
	curl -jkLH "Cookie: oraclelicense=accept-securebackup-cookie" -o java.tar.gz\
     http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_URL_ELEMENT}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz &&\
 	gunzip -c java.tar.gz | tar -xf - -C /opt && rm -f java.tar.gz &&\
 	ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jdk &&\
	# Remove spurious folders not needed (like jre/lib).
 	rm -rf /opt/jdk/*src.zip \
          /opt/jdk/lib/missioncontrol \
          /opt/jdk/lib/visualvm \
          /opt/jdk/lib/*javafx* \
          /opt/jdk/jre/lib/plugin.jar \
          /opt/jdk/jre/lib/ext/jfxrt.jar \
          /opt/jdk/jre/bin/javaws \
          /opt/jdk/jre/lib/javaws.jar \
          /opt/jdk/jre/lib/desktop \
          /opt/jdk/jre/plugin \
          /opt/jdk/jre/lib/deploy* \
          /opt/jdk/jre/lib/*javafx* \
          /opt/jdk/jre/lib/*jfx* \
          /opt/jdk/jre/lib/amd64/libdecora_sse.so \
          /opt/jdk/jre/lib/amd64/libprism_*.so \
          /opt/jdk/jre/lib/amd64/libfxplugins.so \
          /opt/jdk/jre/lib/amd64/libglass.so \
          /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
          /opt/jdk/jre/lib/amd64/libjavafx*.so \
          /opt/jdk/jre/lib/amd64/libjfx*.so &&\
   apk del curl &&\
   rm -rf /var/cache/apk/*

# Install Sonar
RUN dotnet tool install --global dotnet-sonarscanner --version ${SONAR_SCANNER_MSBUILD_VERSION}

COPY SonarQube.Analysis.xml ${SONAR_SCANNER_HOME}/
COPY sonar-scanner.properties ${SONAR_SCANNER_HOME}/sonar-scanner-${EMBEDDED_SONAR_SCANNER_VERSION}/conf/

# This will fail but it'll load/download sonar plugins
RUN dotnet sonarscanner; exit 0

# Install other pipeline tools
COPY --from=pipeline-tools ${TOOLS_HOME}/* ${TOOLS_HOME}/
RUN ln -s ${TOOLS_HOME}/* /usr/local/bin/

# Install MiniCover (test coverage tool)
COPY ./tools/tools.csproj ${MINICOVER_HOME}/
COPY ./tools/dotnet-coverage ${MINICOVER_HOME}/
RUN chmod +x ${MINICOVER_HOME}/dotnet-coverage
RUN ln -s ${MINICOVER_HOME}/dotnet-coverage /usr/local/bin/dotnet-coverage

# MiniCover is a C# project
WORKDIR ${MINICOVER_HOME}
RUN dotnet restore --no-cache
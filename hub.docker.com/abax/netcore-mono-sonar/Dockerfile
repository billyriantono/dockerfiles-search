FROM microsoft/dotnet:2.1-sdk

# Install Mono
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF

RUN echo "deb http://download.mono-project.com/repo/debian stable-stretch main"  | tee /etc/apt/sources.list.d/mono-official-stable.list \
  && apt-get update \
  && apt-get install -y mono-devel \
  && rm -rf /var/lib/apt/lists/* /tmp/* \
  && curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe \
  && echo "alias nuget=\"mono /usr/local/bin/nuget.exe\"" | tee ~/.bash_profile
ENV FrameworkPathOverride=/usr/lib/mono/4.6.1-api/

# set up environment
ENV SONAR_SCANNER_VERSION=3.2.0.1227 \
	SONAR_SCANNER_MSBUILD_VERSION=4.3.0.1333 \
	SONAR_SCANNER_MSBUILD_PATH=/opt/sonar-scanner-msbuild \
	DOTNET_BUILD_DIR=/build_dir
	
# This part is copied from the official OpenJDK JRE 8 Dockerfile 
# Source: https://github.com/docker-library/openjdk/blob/master/8-jre/slim/Dockerfile
RUN apt-get update && apt-get install -y --no-install-recommends \
		bzip2 \
		unzip \
		xz-utils \
	&& rm -rf /var/lib/apt/lists/*

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home

# do some fancy footwork to create a JAVA_HOME that's cross-architecture-safe
RUN ln -svT "/usr/lib/jvm/java-8-openjdk-$(dpkg --print-architecture)" /docker-java-home
ENV JAVA_HOME /docker-java-home/jre

RUN set -ex; \
	\
# deal with slim variants not having man page directories (which causes "update-alternatives" to fail)
	if [ ! -d /usr/share/man/man1 ]; then \
		mkdir -p /usr/share/man/man1; \
	fi; \
	\
    echo 'deb http://deb.debian.org/debian stretch-backports main' \
      > /etc/apt/sources.list.d/stretch-backports.list; \
	apt-get update -y;\
	apt-get install -t \
		stretch-backports \
		openjdk-8-jre-headless \
		ca-certificates-java -y; \
	rm -rf /var/lib/apt/lists/*; \
	\
# verify that "docker-java-home" returns what we expect
	[ "$(readlink -f "$JAVA_HOME")" = "$(docker-java-home)" ]; \
	\
# update-alternatives so that future installs of other OpenJDK versions don't change /usr/bin/java
	update-alternatives --get-selections | awk -v home="$(readlink -f "$JAVA_HOME")" 'index($3, home) == 1 { $2 = "manual"; print | "update-alternatives --set-selections" }'; \
# ... and verify that it actually worked for one of the alternatives we care about
	update-alternatives --query java | grep -q 'Status: manual'

# see CA_CERTIFICATES_JAVA_VERSION notes above
RUN /var/lib/dpkg/info/ca-certificates-java.postinst configure

# Download the sonar scanner for msbuild
RUN wget https://github.com/SonarSource/sonar-scanner-msbuild/releases/download/$SONAR_SCANNER_MSBUILD_VERSION/sonar-scanner-msbuild-$SONAR_SCANNER_MSBUILD_VERSION-netcoreapp2.0.zip -O /opt/sonar-scanner-msbuild.zip \
  && mkdir -p $SONAR_SCANNER_MSBUILD_PATH \
  && mkdir -p $DOTNET_BUILD_DIR \
  && unzip /opt/sonar-scanner-msbuild.zip -d $SONAR_SCANNER_MSBUILD_PATH \
  && rm /opt/sonar-scanner-msbuild.zip \
  && chmod -R 775 $SONAR_SCANNER_MSBUILD_PATH \
  && chmod -R 775 $DOTNET_BUILD_DIR

RUN wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 -O /bin/jq \
    && chmod +x /bin/jq

ENV PATH="$SONAR_SCANNER_MSBUILD_PATH:$SONAR_SCANNER_MSBUILD_PATH/sonar-scanner-$SONAR_SCANNER_VERSION/bin:${PATH}"

WORKDIR $DOTNET_BUILD_DIR

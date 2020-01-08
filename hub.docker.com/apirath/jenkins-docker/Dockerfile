FROM jenkins/jenkins:2.197-alpine
# if we want to install via apk
USER root

ENV SONAR_SCANNER_CLI_VERSION 4.1.0.1829
ENV DOTNET_VERSION 3.0.0

# Update apk repositories
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/main" > /etc/apk/repositories \
  && echo "http://dl-2.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
  && echo "http://dl-2.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \

  # Install the latest Docker CE binaries
  && apk update \
  && apk -U --no-cache --allow-untrusted add shadow docker ansible docker-compose kubernetes php maven go nodejs yarn npm py-pip py-setuptools libunwind libunwind-dev libssl1.1 icu-libs libcurl libintl

# Copy Jenkins Plugins
COPY plugins.txt /usr/share/jenkins/plugins.txt

# Update pip and add jenkins to docker group
RUN pip install --upgrade pip \
  # Minimize size
  && rm -rf /var/lib/apt/lists/* /var/cache/apk/* /usr/share/man /tmp/* \
  # Install Jenkins Plugins
  && /usr/local/bin/install-plugins.sh $(cat /usr/share/jenkins/plugins.txt)

# copy custom built plugins
# COPY plugins/*.hpi /usr/share/jenkins/ref/plugins/

# so we can use jenkins cli
COPY config/jenkins.properties /usr/share/jenkins/ref/

# remove executors in master
COPY config/*.groovy /usr/share/jenkins/ref/init.groovy.d/
# COPY config/master-executors.groovy /usr/share/jenkins/ref/init.groovy.d/

# lets configure Jenkins with some defaults
# COPY config/*.xml /usr/share/jenkins/ref/

# drop back to the regular jenkins user - good practice
# USER jenkins

# sonar-scanner-cli: https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/
RUN curl https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_CLI_VERSION}.zip -o sonar-scanner-cli-${SONAR_SCANNER_CLI_VERSION}.zip \
  && unzip sonar-scanner-cli-${SONAR_SCANNER_CLI_VERSION}.zip -d /opt/ \
  && ln -sf /opt/sonar-scanner-${SONAR_SCANNER_CLI_VERSION}/bin/sonar-scanner /opt/sonar-scanner-${SONAR_SCANNER_CLI_VERSION}/bin/sonar-scanner-debug /usr/bin \
  && rm -f sonar-scanner-cli-${SONAR_SCANNER_CLI_VERSION}.zip

# Install .NET Core: https://github.com/dotnet/dotnet-docker/blob/master/3.0/runtime/alpine3.9/amd64/Dockerfile
RUN wget -O dotnet.tar.gz https://dotnetcli.blob.core.windows.net/dotnet/Runtime/$DOTNET_VERSION/dotnet-runtime-$DOTNET_VERSION-linux-musl-x64.tar.gz \
  && dotnet_sha512='a7382fbfabbfe859a66151760f199799d093a88c50a6f2fd97f31a7d6d688d9978526b9637c5e10b95a3155f76d5032cc7f054bb168915eeacf0dd759ada8b54' \
  && echo "$dotnet_sha512  dotnet.tar.gz" | sha512sum -c - \
  && mkdir -p /usr/share/dotnet \
  && tar -C /usr/share/dotnet -xzf dotnet.tar.gz \
  && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
  && rm dotnet.tar.gz \
  && curl https://dot.net/v1/dotnet-install.sh -o /usr/bin/dotnet-install.sh \
  && chmod +x /usr/bin/dotnet-install.sh \
  # Install dotnet sdk v2.1
  && dotnet-install.sh --channel 2.1 --install-dir /usr/share/dotnet/ \
  # Install dotnet sdk v2.2
  && dotnet-install.sh --channel 2.2 --install-dir /usr/share/dotnet/ \
  # Install dotnet sdk v3.0
  && dotnet-install.sh --channel 3.0 --install-dir /usr/share/dotnet/
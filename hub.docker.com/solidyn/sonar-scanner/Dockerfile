FROM openjdk:8-jre-alpine

ENV version=3.0.3.778

LABEL maintainer='Ian Martin <imartin@solidyn.com>' license='MIT' name='sonar-scanner'\
  description='An image of the stock SonarQube scanner tool' url='https://github.com/solidyn/docker' \
  vendor='Solidyn Solutions' version=${version}

RUN apk -Uuv add curl unzip && \
  cd /tmp && \
  curl -kLO https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${version}.zip && \
	unzip -q sonar-scanner-cli-${version}.zip && \
  mv sonar-scanner-${version} /scanner && \
  ln -fsn /scanner/bin/sonar-scanner /usr/bin/sonar-scanner && \
	rm sonar-scanner-cli-${version}.zip && \
  apk --purge -v del unzip curl && \
	rm /var/cache/apk/* && \
  addgroup -g 2391 sonar && \
  adduser -D -u 2391 -G sonar sonar && \
  mkdir -p /src && \
  chown -R sonar: /src

WORKDIR /src
USER sonar
ENTRYPOINT ["sonar-scanner"]
CMD ["--help"]

FROM openjdk:11

ADD ./ymlgen.sh /bin/ymlgen
RUN apt-get update && curl -sL https://deb.nodesource.com/setup_10.x |  bash - && apt-get install -y nodejs wget && \
  wget http://central.maven.org/maven2/io/swagger/codegen/v3/swagger-codegen-cli/3.0.10/swagger-codegen-cli-3.0.10.jar -O swagger-codegen-cli.jar && \
  mv swagger-codegen-cli.jar /var/opt/swagger-codegen.jar && \
  npm install -g redoc-cli && chmod +x /bin/ymlgen && \
  apt-get install python3-pip -y && \
  pip3 install awscli --upgrade

# close to https://github.com/schickling/dockerfiles/tree/master/swagger-ui
FROM maven:3-jdk-7

RUN echo deb http://httpredir.debian.org/debian stable main contrib >/etc/apt/sources.list \
    && echo deb http://security.debian.org/ stable/updates main contrib >>/etc/apt/sources.list \
	&& curl -sL https://deb.nodesource.com/setup_4.x | bash - \
	&& apt-get install -y -q openssl nodejs expect-dev \
	&& apt-get upgrade -y -q \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/swagger-api/swagger-codegen.git
WORKDIR swagger-codegen
RUN mvn -Dmaven.artifact.threads=20 -Dmaven.test.skip=true package

WORKDIR /app
ADD tools/npm-exp.sh npm-exp.sh
RUN chmod u+rwx /app/*.sh
RUN npm set registry https://npm.bsolut.com \
    && npm config set always-auth true \
    && /app/npm-exp.sh "npm login " docker insecure docker@unikrn.com

ENV VERSION "v2.2.6"
ENV FOLDER "swagger-ui-2.2.6"

RUN wget -qO- https://github.com/swagger-api/swagger-ui/archive/$VERSION.tar.gz | tar xvz
RUN cp -r $FOLDER/dist/* . && rm -rf $FOLDER
RUN npm install -g http-server

ADD tools/run.sh run.sh
ENV API_URL "/swagger.json"
ENV API_KEY "**None**"
ENV SWAGGER_YAML "/app/swagger.yaml"
ENV SWAGGER_JSON "/swagger.json"

EXPOSE 80
ENV PORT 80

CMD ["bash", "run.sh"]

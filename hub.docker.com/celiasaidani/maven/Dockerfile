
FROM celiasaidani/maven

RUN mkdir -p /usr/app/src

ONBUILD ADD ./src /usr/app/src
ONBUILD ADD ./pom.xml /usr/app
WORKDIR /usr/app

ONBUILD RUN mvn install

CMD [ "mvn","clean", "test", "package" ]

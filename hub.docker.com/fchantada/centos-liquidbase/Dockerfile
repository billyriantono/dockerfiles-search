FROM fchantada/centos-jdk:latest

ADD https://github.com/liquibase/liquibase/releases/download/liquibase-parent-3.6.1/liquibase-3.6.1-bin.tar.gz /tmp

RUN mkdir /opt/liquibase \
    && tar xzf /tmp/liquibase-3.6.1-bin.tar.gz -C /opt/liquibase \
    && rm /tmp/liquibase-3.6.1-bin.tar.gz

WORKDIR /opt/liquibase

RUN curl -L https://drive.google.com/uc?id=1BFxtiwGoIU0Y82RY6TH1WAbxd5FJQHHu -o /opt/liquibase/lib/snakeyaml-1.18.jar

RUN curl -L https://drive.google.com/uc?id=17vpwl8w_BDsfbsgaz-Bkfr9Qn0Oiicoj -o /opt/liquibase/lib/slf4j-api-1.7.25.jar

RUN curl -L https://drive.google.com/uc?id=180ugXhUn2JWsMW5ZP-IEve0F4yh8fhqY -o /opt/liquibase/lib/mysql-connector-java-6.0.6.jar

RUN curl -L https://drive.google.com/uc?id=1rFNpktOL_iJtDyqgMndHaeCA0PQehvdF -o /opt/liquibase/lib/mssql-jdbc-6.4.0.jre8.jar

RUN curl -L https://drive.google.com/uc?id=1YrUTFKXzsTv_rSA2iFPG67dNzxMJFLHk -o /opt/liquibase/lib/postgresql-42.2.2.jar

ADD changelog_example.yml /opt/liquibase

FROM podbox/java8

# Install Lein
RUN apt-get install -y wget \
    && wget -O bin/lein https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein \
    && chmod a+x bin/lein \
    && bin/lein

RUN mkdir card-app

WORKDIR card-app/

COPY . card-app/

# Build application with Lein
RUN cd card-app \
    && lein uberjar

EXPOSE 8080

CMD ["java", "-jar", "/card-app/target/card-app-0.1.0-SNAPSHOT-standalone.jar"]
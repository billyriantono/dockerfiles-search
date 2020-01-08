FROM ubuntu:12.04

COPY . /src

RUN apt-get update && apt-get install -y openjdk-7-jdk curl && curl -o /bin/lein https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein && chmod a+x /bin/lein && lein && cd /src && lein compile && lein uberjar && rm -rf /var/lib/apt/lists/*

CMD cd /src && java $JVM_OPTS -cp target/helloworld-standalone.jar clojure.main -m hello.world $PORT

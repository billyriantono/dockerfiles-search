FROM openjdk:11

ADD install.sh .
ADD yices yices-sat yices-smt yices-smt2 z3 cvc3 cvc4 /usr/bin/

RUN set -o errexit -o nounset \
    && apt-get update -y \
    && apt-get install -y findutils git wget curl python3-requests unzip zip libgomp1

RUN bash install.sh

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64/
ENV PATH="${PATH}:~/.sdkman/candidates/ant/current/bin/:~/.sdkman/candidates/gradle/current/bin/"

RUN set -o errexit -o nounset \
        && echo "Testing Gradle installation" \
        && java -version \
        && $HOME/.sdkman/candidates/ant/current/bin/ant -version \
        && $HOME/.sdkman/candidates/gradle/current/bin/gradle --version

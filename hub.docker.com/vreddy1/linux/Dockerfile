# Build
FROM openjdk:8-jdk-alpine as builder
ARG sourceVersion=local
LABEL builder=true

WORKDIR /source

COPY ./ ./

#ENV GRADLE_VERSION 4.10
#
#RUN TMPFILE="$(mktemp)" && \
#  wget "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" -O "$TMPFILE" && \
#  unzip "$TMPFILE" -d "/usr/local" && \
#  mv "/usr/local/gradle-${GRADLE_VERSION}" "/usr/local/gradle" && \
#  ln -s "../gradle/bin/gradle" "/usr/local/bin/gradle" && \
#  rm "$TMPFILE"
#
#RUN mkdir ~/.gradle && \
#  echo "org.gradle.daemon=false" > ~/.gradle/gradle.properties
#
#RUN gradle clean build

RUN  ls && \
      chmod +x gradlew && \
     ./gradlew clean build

# App
FROM openjdk:8-jdk-alpine
LABEL builder=false

WORKDIR /deploy

EXPOSE 8080

COPY --from=builder ./source/build/libs/stooge-1.1.0.jar ./

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","stooge-1.1.0.jar"]
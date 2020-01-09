FROM quay.io/bitriseio/android-ndk:alpha
WORKDIR /app

ENV GRADLE_HOME /opt/gradle-4.2.1
ENV PATH $PATH:/opt/gradle-4.2.1/bin

RUN wget -q https://services.gradle.org/distributions/gradle-4.2.1-bin.zip \
    && unzip gradle-4.2.1-bin.zip -d /opt \
    && rm gradle-4.2.1-bin.zip
RUN gradle -v
RUN gradle tasks
RUN gradle wrapper --gradle-version 4.2.1

RUN ./gradlew build --stacktrace
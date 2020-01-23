FROM openjdk:12.0.1-jdk

MAINTAINER Yaroslav Admin "yaroslav.admin@softwerk.se"

# Configure JDK to use not-blocking CSPRNG. See for motivation: http://www.2uo.de/myths-about-urandom/
RUN sed -i 's*securerandom.source=file:/dev/random*securerandom.source=file:/dev/urandom*g' $JAVA_HOME/conf/security/java.security

# Configure working directory
WORKDIR /usr/src/app

CMD ["sleep", "365d"]

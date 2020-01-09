FROM        kevto/ubuntu-typesafe-java8-docker

MAINTAINER  Kevin Berendsen <berendsen.kevin@gmail.com>

# COMMIT PROJECT FILES
ADD         app /root/app
ADD         test /root/test
ADD         conf /root/conf
ADD         public /root/public
ADD         build.sbt /root/
ADD         project/plugins.sbt /root/project/
ADD         project/build.properties /root/project/

# TEST AND BUILD THE PROJECT -- FAILURE WILL HALT IMAGE CREATION
RUN         cd /root; /usr/local/activator/activator stage
RUN         echo "Current map" && pwd
RUN         ls /root
RUN         rm /root/target/universal/stage/bin/*.bat

# TESTS PASSED -- CONFIGURE IMAGE
WORKDIR     /root
#ENTRYPOINT  ["target/universal/stage/bin/play2-docker-hello-world"]
#CMD         ["activator", "run"]
EXPOSE      9000

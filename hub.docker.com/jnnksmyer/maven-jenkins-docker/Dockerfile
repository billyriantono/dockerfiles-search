FROM maven:3-alpine
RUN addgroup -S -g 1000 maven && adduser -S -u 1000 -G maven maven
RUN mkdir -p /home/maven/.m2/repository && chown -R maven /home/maven
USER maven

FROM maven:3-jdk-8-alpine
ADD . /
RUN ./build.sh
ENTRYPOINT ./generate_models.sh

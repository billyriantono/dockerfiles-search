FROM openjdk:8-alpine
RUN wget https://oss.sonatype.org/content/repositories/snapshots/io/swagger/swagger-codegen-cli/3.0.0-SNAPSHOT/swagger-codegen-cli-3.0.0-20180714.172900-89.jar -O codegen-cli.jar
ENTRYPOINT [ "java", "-jar", "codegen-cli.jar" ]

ARG JDK_VERSION=14
FROM openjdk:${JDK_VERSION}-alpine as builder
LABEL maintainer="KeYou <100keyou100@gmail.com>"
LABEL description="This is multi-stage build example."

COPY Test.java /usr/src/myapp/
WORKDIR /usr/src/myapp/
RUN javac Test.java

FROM openjdk:${JDK_VERSION}-alpine
COPY --from=builder /usr/src/myapp/Test.class /java/src/
WORKDIR /java/src/

CMD ["java", "Test"]

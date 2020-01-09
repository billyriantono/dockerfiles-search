FROM openjdk:11-jdk-slim as builder
WORKDIR /etc/chargebee-mirror-service
COPY ./ ./
USER root
RUN chmod +x ./gradlew
RUN ./gradlew build --stacktrace

FROM openjdk:11-jre-slim
COPY --from=builder ./etc/chargebee-mirror-service/build/libs/ .
ENTRYPOINT java \
	-XX:+UseG1GC \
	-XX:+UseStringDeduplication \
	-Xmx$HEAP_SIZE \
	-jar \
	./chargebee-mirror-service.jar
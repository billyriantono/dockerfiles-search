FROM frekele/gradle
COPY . /app
WORKDIR /app
RUN gradle build
ENV JAVA_OPTS=""
EXPOSE 8080:8080
ENTRYPOINT [ "sh", "-c", "/app/run.sh" ]
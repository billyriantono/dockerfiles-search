FROM  openjdk:8-jre-alpine


RUN wget "https://www.languagetool.org/download/LanguageTool-4.0.zip" -O /tmp/langauge-tool.zip

RUN mkdir "/tmp/langauge-tool" && \
    unzip "/tmp/langauge-tool.zip" -d /tmp/langauge-tool && \
    mkdir "/usr/src/" && \
    mv /tmp/langauge-tool/LanguageTool-4.0 /usr/src/app && \
    rm -rf /tmp

COPY ./server.properties /usr/src/app

EXPOSE 8080


WORKDIR /usr/src/app
ENV CONTEXT_PATH=ROOT

CMD [ "java", "-cp", "languagetool-server.jar", "org.languagetool.server.HTTPServer", "--port", "8080", "--public"]
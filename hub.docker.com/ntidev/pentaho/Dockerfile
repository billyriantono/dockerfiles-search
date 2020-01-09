FROM alpine:3.8 as BUILDER
WORKDIR /di
RUN wget https://svwh.dl.sourceforge.net/project/pentaho/Pentaho%208.2/client-tools/pdi-ce-8.2.0.0-342.zip
RUN unzip pdi-ce-8.2.0.0-342.zip
COPY ./jtds-1.3.1.jar data-integration/lib


FROM java:openjdk-8-alpine
WORKDIR /pentaho
COPY --from=BUILDER /di/data-integration data-integration
CMD ["tail", "-f", "/dev/null"]

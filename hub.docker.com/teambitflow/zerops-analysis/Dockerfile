# teambitflow/zerops-analysis
FROM teambitflow/bitflow4j-build:latest as build
WORKDIR /build
COPY pom.xml .
COPY zerops-analysis zerops-analysis

# Install IFTM-anomaly-detection dependencies
WORKDIR /dependencies/iftm
COPY --from=teambitflow/anomaly-detection:latest anomaly-detection/ .
RUN mvn install --non-recursive
RUN cd algorithms && mvn install:install-file -Dfile=anomaly-detection.jar -DpomFile=pom.xml

# Install anomaly-state-analysis dependencies
WORKDIR /dependencies/anomaly-state-analysis
COPY --from=teambitflow/anomaly-state-analysis:latest /compiled/pom.xml .
COPY --from=teambitflow/anomaly-state-analysis:latest /compiled/online-density-estimation online-density-estimation
COPY --from=teambitflow/anomaly-state-analysis:latest /compiled/ode-classification ode-classification
RUN mvn install --non-recursive
RUN cd online-density-estimation && mvn install:install-file -Dfile=online-density-estimation.jar -DpomFile=pom.xml
RUN cd ode-classification && mvn install:install-file -Dfile=ode-classification.jar -DpomFile=pom.xml

WORKDIR /build
ENV MVN_ARGS="-B -Dorg.slf4j.simpleLogger.log.org.apache.maven.cli.transfer.Slf4jMavenTransferListener=warn"
RUN mvn install --non-recursive $MVN_ARGS

RUN cd zerops-analysis && mvn package $MVN_ARGS && \
    cp target/zerops-analysis-*-jar-with-dependencies.jar target/zerops-analysis.jar

# final image 
FROM openjdk:11-jre-slim
WORKDIR /zerops
COPY --from=build /build/zerops-analysis/target/zerops-analysis.jar .
COPY --from=teambitflow/go-bitflow:static /bitflow-pipeline /
ENTRYPOINT ["java", "-jar", "zerops-analysis.jar", "-P", "zerops", "-P", "bitflow4j"]


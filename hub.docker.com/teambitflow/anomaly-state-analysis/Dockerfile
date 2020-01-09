FROM maven:3.6-jdk-8 as build

WORKDIR /build
COPY . .
RUN mvn install
RUN mkdir ../ode-classification && mkdir ../online-density-estimation
RUN cp online-density-estimation/target/online-density-estimation-*.jar ../online-density-estimation/online-density-estimation.jar && \
    cp online-density-estimation/pom.xml ../online-density-estimation/pom.xml
RUN cp ode-classification/target/ode-classification-*.jar ../ode-classification/ode-classification.jar && \
    cp ode-classification/pom.xml ../ode-classification/pom.xml

FROM maven:3.6-alpine
WORKDIR /compiled
COPY --from=build /online-density-estimation online-density-estimation 
COPY --from=build /ode-classification ode-classification
COPY --from=build /build/pom.xml .

FROM openjdk:8-jre-alpine

# Install curl for healthchecks
RUN apk add --update \
    curl \
    maven \
    && rm -rf /var/cache/apk/*

# Add a settings file for the Maven build
ADD settings.xml /hapi-fhir/hapi-fhir-cli/settings.xml

# Download the archive and extract it
RUN curl -Ls https://github.com/jamesagnew/hapi-fhir/archive/v2.5.tar.gz \
    | tar xfzv - -C /hapi-fhir --strip-components=1 && \

    # Update the server configuration files to disable search caching
    find /hapi-fhir/hapi-fhir-cli/hapi-fhir-cli-jpaserver/src/main/java/ca/uhn/fhir/jpa/demo \
        -name "FhirServerConfig*.java" \
        -exec sed -i 's/DaoConfig retVal = new DaoConfig();/DaoConfig retVal = new DaoConfig();retVal.setReuseCachedSearchResultsForMillis(null);/g' {} + && \

    # Move to the CLI project directory.
    cd /hapi-fhir/hapi-fhir-cli && \

    # Build it!
    mvn install -q -s /hapi-fhir/hapi-fhir-cli/settings.xml && \

    # Move the built jar out of the build directory
    mv /hapi-fhir/hapi-fhir-cli/hapi-fhir-cli-app/target/hapi-fhir-cli.jar /root/hapi-fhir-cli.jar && \

    # Cleanup
    rm -rf /hapi-fhir

WORKDIR /root

# Set the port for HAPI-FHIR
ENV HAPI_FHIR_PORT 8080

HEALTHCHECK CMD curl http://localhost:$HAPI_FHIR_PORT/baseDstu3/Patient

EXPOSE $HAPI_FHIR_PORT

CMD java -jar hapi-fhir-cli.jar run-server -p $HAPI_FHIR_PORT
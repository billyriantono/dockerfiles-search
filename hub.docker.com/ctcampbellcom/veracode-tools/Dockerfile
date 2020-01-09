FROM openjdk:10

RUN apt-get update && apt-get install -y zip jq && mkdir /veracode

WORKDIR /veracode

RUN VERACODE_WRAPPER_VERSION=$(curl -sS "https://search.maven.org/solrsearch/select?q=g:%22com.veracode.vosp.api.wrappers%22&rows=20&wt=json" | jq -r '.["response"]["docs"][0].latestVersion') \
  && curl -sS -o veracode-wrapper.jar "https://repo1.maven.org/maven2/com/veracode/vosp/api/wrappers/vosp-api-wrappers-java/${VERACODE_WRAPPER_VERSION}/vosp-api-wrappers-java-${VERACODE_WRAPPER_VERSION}.jar"

RUN curl -sS -O https://downloads.veracode.com/securityscan/gl-scanner-java-LATEST.zip && unzip gl-scanner-java-LATEST.zip gl-scanner-java.jar && rm -f gl-scanner-java-LATEST.zip

FROM clojure:lein-2.7.1

ENV OS=linux
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
      graphviz software-properties-common build-essential nodejs chromium && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

WORKDIR /

# Used by device-bridge builds
# Not using version provided by apt as it's too old and having issues
# (with 'mvn deploy's to our maven repository)
ENV MVN_VERSION=3.6.2
ENV MVN_SHA512SUM=d941423d115cd021514bfd06c453658b1b3e39e6240969caf4315ab7119a77299713f14b620fb2571a264f8dff2473d8af3cb47b05acf0036fc2553199a5c1ee

RUN curl -o mvn.tar.gz "https://www-eu.apache.org/dist/maven/maven-3/$MVN_VERSION/binaries/apache-maven-$MVN_VERSION-bin.tar.gz" && \
    sha512sum -c <( echo ${MVN_SHA512SUM} mvn.tar.gz ) && \
    tar xzf mvn.tar.gz && \
    rm -f mvn.tar.gz && \
    mv "/apache-maven-$MVN_VERSION" /apache-maven

# https://cloud.google.com/sdk/docs/quickstart-linux
ENV GCLOUD_VERSION=240.0.0
ENV GCLOUD_SHA256SUM=5b7ad4e2632c77d5643162af6e1a586d22c5da82fe4e2ec18c411c831c6f5a44
ENV GCLOUD_ARCH=x86_64

RUN curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz && \
    echo "${GCLOUD_SHA256SUM}  google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz" > google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz.sha256 && \
    sha256sum -c google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz.sha256 && \
    tar xzf google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz  && \
    rm -f google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz && \
    rm -f google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz.sha256 # && \
    /google-cloud-sdk/bin/gcloud config set component_manager/disable_update_check true && \
    /google-cloud-sdk/bin/gcloud config set core/disable_usage_reporting true && \
    /google-cloud-sdk/bin/gcloud components install alpha beta cloud_sql_proxy cloud-build-local docker-credential-gcr kubectl

# OWASP Dependency Check tool installation
# https://jeremylong.github.io/DependencyCheck/dependency-check-cli/index.html
ENV OWASP_DEPENDENCY_CHECK_VERSION=5.1.1
RUN curl -O -L "https://dl.bintray.com/jeremy-long/owasp/dependency-check-${OWASP_DEPENDENCY_CHECK_VERSION}-release.zip" && \
    unzip dependency-check-${OWASP_DEPENDENCY_CHECK_VERSION}-release.zip && \
    rm -f dependency-check-${OWASP_DEPENDENCY_CHECK_VERSION}-release.zip

ENV PATH /google-cloud-sdk/bin:/dependency-check/bin:/apache-maven/bin:$PATH

RUN useradd -ms /bin/bash pipelines-builder

USER pipelines-builder

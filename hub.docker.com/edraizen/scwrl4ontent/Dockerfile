FROM openjdk:8 as builder

ENV BUILD_HOME="/opt/builder"
ENV ORBEON_URL="https://github.com/orbeon/orbeon-forms/releases/download/tag-release-2018.2.1-ce/orbeon-2018.2.1.201902072242-CE.zip"

WORKDIR ${BUILD_HOME}
COPY . .

RUN apt-get update \
    && apt-get install -y --no-install-recommends unzip curl \
    && curl -OL ${ORBEON_URL} \
    && unzip *.zip \
    && mkdir -p build/orbeon \
    && unzip orbeon*/orbeon.war -d build/orbeon \
    && mkdir -p build/orbeon/xforms-jsp/mei-form/ \ 
    && cp mei_form.jsp build/orbeon/xforms-jsp/mei-form/index.jsp \
    && jar cf orbeon.war -C build/orbeon/ .

FROM tomcat:8

COPY --from=builder /opt/builder/orbeon.war /usr/local/tomcat/webapps/

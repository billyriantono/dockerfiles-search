FROM cheempz/java_appservers:j8_tomcat7

ENV STACK_APPS='test-spring-mvc4 test-xml-soap'

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*

WORKDIR $CATALINA_HOME/webapps

RUN for app_name in $STACK_APPS ; do \
        curl -L -o ${app_name}.war https://s3.amazonaws.com/apm-qa-automation/java/compiled-test-apps/${app_name}.war-latest ; \
    done

WORKDIR $CATALINA_HOME
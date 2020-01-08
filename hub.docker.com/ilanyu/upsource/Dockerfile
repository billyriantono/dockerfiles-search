FROM jetbrains/upsource:2019.1.1460

MAINTAINER ilanyu <lanyu19950316@gmail.com>

COPY com.lanyus.crack.upsource.jar /opt/upsource/lib/ext/com.lanyus.crack.upsource.jar

USER root

RUN sed -e '/#!\/bin\/bash/a export JAVA_TOOL_OPTIONS=-Xbootclasspath/p:/opt/upsource/lib/ext/com.lanyus.crack.upsource.jar' -i /run.sh

USER 13001:13001

VOLUME /opt/upsource/data /opt/upsource/conf /opt/upsource/logs /opt/upsource/backups

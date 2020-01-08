FROM jetbrains/youtrack:2019.2.56594

MAINTAINER ilanyu <lanyu19950316@gmail.com>

COPY com.lanyus.crack.upsource.jar /opt/youtrack/lib/ext/com.lanyus.crack.upsource.jar

USER root

RUN sed -e '/#!\/bin\/bash/a export JAVA_TOOL_OPTIONS=-Xbootclasspath/p:/opt/youtrack/lib/ext/com.lanyus.crack.upsource.jar' -i /run.sh

USER 13001:13001

VOLUME /opt/youtrack/data /opt/youtrack/conf /opt/youtrack/logs /opt/youtrack/backups

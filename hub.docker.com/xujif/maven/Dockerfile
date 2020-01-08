FROM maven:3-jdk-11

# add maven mirror
RUN sed -i 'N;148i<mirror>\n<id>aliyun</id>\n<name>aliyun maven</name>\n<url>https://maven.aliyun.com/repository/central</url>\n<mirrorOf>central</mirrorOf>\n</mirror>' /usr/share/maven/conf/settings.xml

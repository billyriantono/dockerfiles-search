FROM openjdk:11-jre
COPY post-bulletins-4.4.2 /opt/post_bulletins
VOLUME /bulletins
WORKDIR /opt/post_bulletins
ENTRYPOINT ["java", "-jar", "jruby-complete.jar", "post_bulletins.rb"]
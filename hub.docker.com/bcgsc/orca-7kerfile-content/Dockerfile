FROM delitescere/jdk

ONBUILD ADD stubby.yml /usr/local/stubby.yml

RUN wget http://central.maven.org/maven2/io/github/azagniotov/stubby4j/6.0.2/stubby4j-6.0.2.jar -O /usr/local/stubby4j.jar

EXPOSE 8889 8882

CMD java -jar /usr/local/stubby4j.jar -d /usr/local/stubby.yml -l 0.0.0.0 -w -s $STUBBY_PORT

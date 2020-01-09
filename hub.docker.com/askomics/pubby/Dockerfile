FROM tomcat
MAINTAINER Xavier Garnier "xavier.garnier@irisa.fr"

RUN wget http://wifo5-03.informatik.uni-mannheim.de/pubby/download/pubby-0.3.3.zip
RUN unzip pubby-0.3.3.zip
RUN cp -r pubby-0.3.3/webapp webapps/pubby
COPY simple.ttl webapps/pubby/WEB-INF/config.ttl
COPY prefixes.n3 webapps/pubby/WEB-INF/prefixes.n3
COPY setTTL.sh .
RUN chmod +x setTTL.sh
COPY setPrefixes.sh .
RUN chmod +x setPrefixes.sh
CMD ./setTTL.sh webapps/pubby/WEB-INF/config.ttl && ./setPrefixes.sh webapps/pubby/WEB-INF/prefixes.n3 && catalina.sh run

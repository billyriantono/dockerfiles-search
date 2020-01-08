FROM openjdk:8
ADD https://github.com/ffc-nectec/api/releases/download/1.0.1/ffc-api.jar /srv/ffc-api.jar
CMD java -server -Xmx200m -Xss512k -Dfile.encoding=UTF-8 -jar /srv/ffc-api.jar -port 80

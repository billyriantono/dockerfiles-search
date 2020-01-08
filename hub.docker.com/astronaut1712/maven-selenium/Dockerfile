FROM markhobson/maven-chrome

COPY pom.xml /app/pom.xml

RUN mvn -f /app/pom.xml  -T 4 install

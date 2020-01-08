FROM maven:3.6.1
COPY ./jar/Excel_Parameter_Updated.jar ./jar/pCloudy-java-connector-11.0.5-jar-with-dependencies.jar ./jar/ACATS-2.0.2-tests.jar ./
RUN mvn -U install:install-file -Dfile=Excel_Parameter_Updated.jar -DgroupId=com.hw -DartifactId=cuc-framework -Dversion=1.0-SNAPSHOT -Dpackaging=jar
RUN mvn -U install:install-file -Dfile=pCloudy-java-connector-11.0.5-jar-with-dependencies.jar -DgroupId=pCloudy-java-connector -DartifactId=pCloudy-java-connector -Dversion=11.0.5 -Dpackaging=jar
RUN mvn -U install:install-file -Dfile=ACATS-2.0.2-tests.jar -DgroupId=com.acats.core -DartifactId=ACATS -Dversion=2.0.2 -Dpackaging=jar
RUN rm *.jar
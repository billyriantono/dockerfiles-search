FROM gradle
WORKDIR /usr/local/bin


RUN wget https://github.com/NativeScript/android-dts-generator/archive/2.0.tar.gz -O android-dts-generator.tar.gz

RUN tar xvf android-dts-generator.tar.gz
RUN mv android-dts-generator-2.0 android-dts-generator 
RUN rm android-dts-generator.tar.gz

WORKDIR /usr/local/bin/android-dts-generator/dts-generator
RUN ./gradlew build & ./gradlew jar
  
ENTRYPOINT [ "java", "-jar", "/usr/local/bin/android-dts-generator/dts-generator/build/libs/dts-generator.jar" ]
CMD ["-input", "/usr/src/jarFolder", "-output", "/usr/src/jarFolder/dts"]
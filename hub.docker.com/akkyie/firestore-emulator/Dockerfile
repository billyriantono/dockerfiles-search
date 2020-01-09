FROM openjdk

ADD https://firebase.google.com/docs/firestore/downloads/cloud-firestore-emulator.jar ./cloud-firestore-emulator.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "./cloud-firestore-emulator.jar"]

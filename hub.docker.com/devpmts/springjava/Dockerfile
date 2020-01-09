FROM devpmts/remotejre
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom -XXaltjvm=dcevm -javaagent:/hotswap-agent.jar","-jar","/app.jar"]


FROM prom/cloudwatch-exporter:latest

RUN apt-get update && apt-get install -y wget && apt-get clean && rm -rf /var/lib/{apt,dpkg,cache,log}/

EXPOSE 9106

ENTRYPOINT [ "java", "-jar", "/cloudwatch_exporter.jar", "9106"]
CMD ["/config/config.yml"]

FROM openjdk:8-alpine

WORKDIR /vocbench3-data/semanticturkey-6.0/bin

# The VocBench3 start script does not run in the foreground. To keep the process alive, we're using /bin/sh.
CMD ./start && /bin/sh
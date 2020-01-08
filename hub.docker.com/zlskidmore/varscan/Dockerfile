# work from latest LTS ubuntu release
FROM ubuntu:18.04

# set the environment variables
ENV version 2.4.2

# run update
RUN apt-get update -y && apt-get install -y \
    openjdk-8-jre \
    wget \
    libnss-sss \
    curl \
    vim \
    less

# download varscan and change permissions
WORKDIR /usr/local/bin
RUN wget https://github.com/dkoboldt/varscan/releases/download/${version}/VarScan.v${version}.jar

# set default command to print help
CMD ["java", "-jar", "/usr/local/bin/VarScan.v${version}.jar"]

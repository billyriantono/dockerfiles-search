FROM openjdk:8u181-jdk-slim-stretch
LABEL maintainer="Ivan Pashchenko <ivan.pashchenko@jetbrains.com>"

RUN apt-get update && apt-get install -y --no-install-recommends \
        maven \
        openjfx \
	&& rm -rf /var/lib/apt/lists/*

# RUN apt-get update && apt-get install -y --no-install-recommends \
#         git \
#         mc \
# 	&& rm -rf /var/lib/apt/lists/*

# RUN git clone https://github.com/JetBrains/azure-tools-for-intellij.git --branch 182
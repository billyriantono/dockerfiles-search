FROM ubuntu:19.10

ENV PATH="/opt/gradle/gradle-5.6/bin:${PATH}"

RUN apt-get update && apt-get install -y --no-install-recommends openjdk-12-jdk wget unzip gcc g++ && \
  wget -O /gradle-5.6-bin.zip https://services.gradle.org/distributions/gradle-5.6-bin.zip && \
	mkdir /opt/gradle && unzip -d /opt/gradle /gradle-5.6-bin.zip && \
	export PATH=$PATH:/opt/gradle/gradle-5.6/bin && \
	apt-get remove -y wget unzip && apt-get autoremove -y && apt-get clean -y \
	&& rm -rf /var/lib/apt/lists/*
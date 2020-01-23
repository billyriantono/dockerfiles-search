FROM openjdk:8

# Install bower
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && apt-get update && apt-get install -y nodejs zip
RUN npm i -g bower

# Install pip
RUN wget "https://bootstrap.pypa.io/get-pip.py" && python get-pip.py && rm get-pip.py
# Install boto3
RUN pip install boto3

# Add Grails 2.4.4
RUN mkdir -p ~/.grails/wrapper/2.4.4 && wget "http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-2.4.4.zip" && unzip grails-2.4.4.zip -d ~/.grails/wrapper/2.4.4 && rm grails-2.4.4.zip
# Add Grails 2.5.0
RUN mkdir -p ~/.grails/wrapper/2.5.0 && wget "http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-2.5.0.zip" && unzip grails-2.5.0.zip -d ~/.grails/wrapper/2.5.0 && rm grails-2.5.0.zip
# Add Grails 2.5.1
RUN mkdir -p ~/.grails/wrapper/2.5.1 && wget "http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-2.5.1.zip" && unzip grails-2.5.1.zip -d ~/.grails/wrapper/2.5.1 && rm grails-2.5.1.zip
# Add Grails 3.3.1
RUN mkdir -p ~/.grails/wrapper/3.3.1 && wget "https://github.com/grails/grails-core/releases/download/v3.3.1/grails-3.3.1.zip" && unzip grails-3.3.1.zip -d ~/.grails/wrapper/3.3.1 && rm grails-3.3.1.zip

# Add Gradle 2.9
RUN mkdir -p ~/.gradle/wrapper/dists/gradle-2.9-all/1aw2ic01pldw5fkvoq6t1fsz4 && wget "https://services.gradle.org/distributions/gradle-2.9-all.zip" && unzip gradle-2.9-all.zip -d ~/.gradle/wrapper/dists/gradle-2.9-all/1aw2ic01pldw5fkvoq6t1fsz4 && mv gradle-2.9-all.zip ~/.gradle/wrapper/dists/gradle-2.9-all/1aw2ic01pldw5fkvoq6t1fsz4/ && touch ~/.gradle/wrapper/dists/gradle-2.9-all/1aw2ic01pldw5fkvoq6t1fsz4/gradle-2.9-all.zip.lck && touch ~/.gradle/wrapper/dists/gradle-2.9-all/1aw2ic01pldw5fkvoq6t1fsz4/gradle-2.9-all.zip.ok
# Add Gradle 3.5
RUN mkdir -p ~/.gradle/wrapper/dists/gradle-3.5-all/exhrs6ca08n232b14ue48lbye && wget "https://services.gradle.org/distributions/gradle-3.5-all.zip" && unzip gradle-3.5-all.zip -d ~/.gradle/wrapper/dists/gradle-3.5-all/exhrs6ca08n232b14ue48lbye && mv gradle-3.5-all.zip ~/.gradle/wrapper/dists/gradle-3.5-all/exhrs6ca08n232b14ue48lbye/ && touch ~/.gradle/wrapper/dists/gradle-3.5-all/exhrs6ca08n232b14ue48lbye/gradle-3.5-all.zip.lck && touch ~/.gradle/wrapper/dists/gradle-3.5-all/exhrs6ca08n232b14ue48lbye/gradle-3.5-all.zip.ok

# Add sonar-scanner
RUN wget "https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.0.3.778-linux.zip" && unzip sonar-scanner-cli-3.0.3.778-linux.zip -d /root/ && ln -s /root/sonar-scanner-3.0.3.778-linux/bin/sonar-scanner /usr/local/bin/ && rm sonar-scanner-cli-3.0.3.778-linux.zip

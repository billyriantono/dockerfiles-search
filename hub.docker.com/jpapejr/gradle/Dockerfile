FROM websphere-liberty:webProfile7
MAINTAINER John Pape <jpapejr@icloud.com>

RUN wget https://services.gradle.org/distributions/gradle-2.13-all.zip && \
    unzip gradle-2.13-all.zip && \
    ln -s /gradle-2.13/bin/gradle /usr/local/bin/gradle
    

EXPOSE 9080 9443 8080

ENTRYPOINT ["/bin/bash"]

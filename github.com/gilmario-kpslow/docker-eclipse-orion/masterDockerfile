FROM openjdk:15-jdk-oracle

WORKDIR /opt
    
RUN wget https://www.eclipse.org/downloads/download.php?file=/orion/drops/R-20.0-201903291844/eclipse-orion-20.0.0S1-linux.gtk.x86_64.zip&mirror_id=576
    && unzip eclipse-orion-20.0.0S1-linux.gtk.x86_64.zip

EXPOSE 8080

ENTRYPOINT ["/opt/eclipse/orion"]
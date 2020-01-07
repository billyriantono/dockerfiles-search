FROM java:8


LABEL io.k8s.description="Java Application Builder" \
    io.k8s.display-name="maven 3.1.1 jdk-8 builder" \
    io.openshift.expose-services="8080:http" \
    io.openshift.tags="builder,webserver,html,java" \
    # this label tells s2i where to find its mandatory scripts
    # (run, assemble, save-artifacts)
    io.openshift.s2i.scripts-url="image:///usr/libexec/s2i"

# Copy the S2I scripts to /usr/libexec/s2i since we set the label that way
COPY  ./s2i/bin/ /usr/libexec/s2i/

RUN wget -q -O - https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.1.1/apache-maven-3.1.1-bin.tar.gz | tar xzf - -C /opt
ENV PATH $PATH:/opt/apache-maven-3.1.1/bin
RUN mkdir -p /opt/app/src && \
    mkdir -p /opt/app/bin && \
    chown -R 1001:0 /opt/app && \
    chown -R 1001:0 $HOME && \
    chmod -R ug+rw /opt/app 

USER 1001

# Modify the usage script in your application dir to inform the user how to run
# this image.
CMD ["/usr/libexec/s2i/usage"]


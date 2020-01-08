FROM alien6/s2i-alpine-node
LABEL "io.openshift.s2i.build.commit.ref"="master" \
      "io.openshift.s2i.build.commit.message"="changing path name" \
      "io.openshift.s2i.build.source-location"="https://github.com/Coopyrightdmin/teachable-machine.git" \
      "io.openshift.s2i.build.image"="alien6/s2i-alpine-node" \
      "io.openshift.s2i.build.commit.author"="Alien6 <contact@alien6.com>"

USER root

COPY .s2i/bin /tmp/scripts
COPY . /tmp/src

RUN chown -R 1001:0 /tmp/scripts /tmp/src &&\
    chmod +x /tmp/scripts/assemble &&\
    chmod +x /usr/libexec/s2i/run

USER 1001
RUN /tmp/scripts/assemble

EXPOSE 3000
CMD /usr/libexec/s2i/run
FROM java

MAINTAINER Potiguar Faga <potz@potz.me>

RUN apt-get update && \
    apt-get install -y curl less git-core && \
    curl -o /bin/jgit https://repo.eclipse.org/content/groups/releases//org/eclipse/jgit/org.eclipse.jgit.pgm/4.3.1.201605051710-r/org.eclipse.jgit.pgm-4.3.1.201605051710-r.sh && \
    apt-get purge -y curl && \
    chmod +x /bin/jgit && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME /repo
WORKDIR /repo

ENTRYPOINT [ "/bin/jgit" ]

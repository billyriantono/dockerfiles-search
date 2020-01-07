FROM codenvy/ubuntu_jdk8:latest

RUN mkdir /home/user/bin
ENV PATH /home/user/bin:$PATH
RUN echo "export PATH=$PATH" >> /home/user/.bashrc

RUN wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -O /home/user/bin/lein && \
    wget https://github.com/boot-clj/boot-bin/releases/download/latest/boot.sh -O /home/user/bin/boot && \
    chmod 755 /home/user/bin/lein && chmod 755 /home/user/bin/boot && \
    /home/user/bin/lein && \
    /home/user/bin/boot && /home/user/bin/boot && \
    timeout 30 /home/user/bin/lein repl :headless ; \
    /bin/cat /dev/null

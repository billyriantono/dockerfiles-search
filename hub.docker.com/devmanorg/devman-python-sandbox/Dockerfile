FROM ubuntu:18.04
RUN mkdir /app
COPY gotty /app
COPY index.html /app
RUN chmod +x /app/gotty
RUN apt-get update && apt-get install -y \
            curl \
            vim \
            git \
            nano \
            python2.7 \
            python3.6 \
            locales
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python2.7 get-pip.py
RUN pip install supervisor                     
RUN mkdir -p /var/log/supervisor && \
    mkdir -p /etc/supervisor/conf.d
RUN chmod -R o+rw /var/log/supervisor && \
    chmod -R o+rw /var/run
COPY supervisord.conf /etc/supervisor/supervisord.conf
RUN useradd -d /home/devman -m -s /bin/bash devman
RUN ln -s /usr/bin/python3.6 /usr/bin/python
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8 
ENV TERM xterm-256color
RUN echo shopt -s histappend >> /home/devman/.bashrc
ENV PROMPT_COMMAND history -a;$PROMPT_COMMAND
USER devman
WORKDIR /home/devman
EXPOSE 8081
CMD ["/usr/local/bin/supervisord"]


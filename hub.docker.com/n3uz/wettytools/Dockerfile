FROM n3uz/wettytools:base
RUN git clone https://github.com/lijiejie/subDomainsBrute.git /app/subdomainsbrute && \
    pip install dnspython gevent && \
    chmod +x /app/subdomainsbrute/subDomainsBrute.py && \
    mv /app/subdomainsbrute/subDomainsBrute.py /app/subdomainsbrute/subDomainsBrute && \
    chown -R term.term /app/subdomainsbrute/
RUN echo "cd /app/subdomainsbrute" >> /home/term/.bashrc
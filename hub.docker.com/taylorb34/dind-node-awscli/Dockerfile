FROM docker:stable
RUN apk add bash git nodejs npm python3 curl
RUN node --version && \
    npm --version && \
    git --version && \
    python3 --version && \
    pip3 --version && \
    curl --version
RUN pip3 install awscli
RUN curl -sL https://sentry.io/get-cli/ | bash
CMD ["bash"]

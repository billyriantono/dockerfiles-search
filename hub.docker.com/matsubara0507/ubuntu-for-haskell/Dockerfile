FROM fpco/ubuntu-with-libgmp
RUN apt-get update && apt-get install -y \
    ca-certificates \
    git \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN git config --global user.email "bot@example.com" \
 && git config --global user.name "Bot"

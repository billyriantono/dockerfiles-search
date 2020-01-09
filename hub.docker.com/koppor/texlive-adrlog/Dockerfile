FROM koppor/texlive

# we additionally need adr-log offered via npm
RUN apt-get update -qq && apt-get install -y --no-install-recommends npm nodejs-legacy && \
    rm -rf /var/lib/apt/lists/* && \
    npm install -g adr-log

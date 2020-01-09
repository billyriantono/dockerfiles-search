# docker build -t cyrilbouvier/ci-latex .
FROM aergus/latex 

RUN apt-get update && \
    apt-get install -y gnuplot xsltproc rubber biber dspdfviewer && \
    # Remove more unnecessary stuff
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

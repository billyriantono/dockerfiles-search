FROM mediawiki:latest

RUN apt-get update && apt-get install -y \
        # Add packages necessary for PdfHandler
        ghostscript \
        poppler-utils \
    --no-install-recommends && rm -r /var/lib/apt/lists/*

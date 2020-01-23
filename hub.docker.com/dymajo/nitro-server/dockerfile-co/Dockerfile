FROM conoria/alpine-pandoc:latest

WORKDIR /work

RUN mkdir -p .pandoc

RUN wget https://gist.githubusercontent.com/griffin-stewie/9755783/raw/13cf5c04803102d90d2457a39c3a849a2d2cc04b/github.css

CMD ["pandoc", "-s", "--self-contained", "-c", "github.css"]
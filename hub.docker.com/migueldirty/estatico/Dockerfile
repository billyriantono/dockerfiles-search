FROM haskell
LABEL maintainer="Michal Idziorek <m.i@gmx.at>"
WORKDIR /estatico
COPY ./ /estatico/
RUN stack build
ENTRYPOINT ["stack","run","estatico","--"]
CMD [""]

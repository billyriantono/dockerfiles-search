FROM haskell:8.4.3
RUN mkdir /build
COPY . /build/
WORKDIR /build/
RUN stack build
RUN stack install --local-bin-path .

FROM ubuntu
COPY --from=0 /build/hello-world-container-exe /
EXPOSE 3000
CMD /hello-world-container-exe

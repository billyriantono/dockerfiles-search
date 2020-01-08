FROM perl:5-threaded
RUN cpan Cache::File
RUN cpan Travel::Status::DE::HAFAS
RUN cpan Travel::Status::DE::IRIS
RUN cpan Mojolicious
RUN cpan File::Slurp
RUN cpan Mojolicious::Plugin::BrowserDetect

WORKDIR /usr/app

COPY . .

CMD ["perl", "index.pl", "daemon"]


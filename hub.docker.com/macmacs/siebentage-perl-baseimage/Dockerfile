FROM perl:5.20

RUN perl -MCPAN -e 'my $c = "CPAN::HandleConfig"; $c->load(doit => 1, autoconfig => 1); $c->edit(prerequisites_policy => "follow"); $c->edit(build_requires_install_policy => "yes"); $c->commit'

# cpan statements as unique RUN command for debuging cpan errors

RUN cpan -fi File::Spec && \
    cpan -fi HTML::Strip && \
    cpan -fi JSON && \
    cpan -fi MP3::Tag && \
    cpan -fi inc::latest && \
    cpan -Ti POSIX URI::Encode && \
    cpan -fi Unicode::String && \
    cpan -fi WWW::Mechanize && \
    cpan -if LWP::Protocol::https

CMD [ "perl", -v]

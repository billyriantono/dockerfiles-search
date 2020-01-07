FROM perl:slim

ENV HOME /opt/opan/
ENV PATH="/opt/opan/local/bin${PATH:+:${PATH}}"
ENV PERL5LIB="/opt/opan/local/lib/perl5${PERL5LIB:+:${PERL5LIB}}"
ENV PERL_LOCAL_LIB_ROOT="/opt/opan/local${PERL_LOCAL_LIB_ROOT:+:${PERL_LOCAL_LIB_ROOT}}"
ENV PERL_MB_OPT="--install_base \"/opt/opan/local\""
ENV PERL_MM_OPT="INSTALL_BASE=/opt/opan/local"

RUN useradd --system --home-dir ${HOME} --create-home --shell /sbin/nologin -c "Docker image user"  opan
WORKDIR ${HOME}
USER opan

ADD cpanfile .
RUN cpanm -n -v --installdeps .
ADD opan_entrypoint.pl .
RUN mkdir -p pans

EXPOSE 3000
ENTRYPOINT ["./opan_entrypoint.pl"]
CMD ["prefork"]

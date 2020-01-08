FROM asciidoctor/docker-asciidoctor

ARG asciidoctor_pdf_cjk_version=0.1.3

ENV ASCIIDOCTOR_PDF_CJK_VERSION=${asciidoctor_pdf_cjk_version}

RUN gem install --no-document "asciidoctor-pdf-cjk:${ASCIIDOCTOR_PDF_CJK_VERSION}"

CMD ["/bin/bash"]
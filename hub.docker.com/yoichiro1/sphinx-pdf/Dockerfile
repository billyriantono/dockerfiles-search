FROM sphinxjp/sphinx-users.jp

RUN echo "deb http://deb.debian.org/debian jessie main" > /etc/apt/sources.list &&\
    echo "deb http://security.debian.org jessie/updates main" >> /etc/apt/sources.list &&\
    apt-get update &&\
    apt-get install -y texlive texlive-lang-cjk latexmk &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* &&\
    pip install sphinx_rtd_theme

CMD bash

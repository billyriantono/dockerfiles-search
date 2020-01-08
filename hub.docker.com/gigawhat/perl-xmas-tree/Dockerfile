FROM perl

RUN cpanm -n Acme::POE::Tree

CMD /usr/local/bin/perl -MAcme::POE::Tree -e 'Acme::POE::Tree->new()->run()'

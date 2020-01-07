FROM pwilga/pycikon:latest
MAINTAINER Piotr Wilga <pwilga@gmail.com>

#Install python packages
RUN pip3 install \
    coverage \
    django \
    django-extensions \
    django-nose \
    djangorestframework \
    drf-nested-routers \
    ipython \
    psycopg2-binary \
    python-dateutil \
    netifaces

RUN apt-get update && apt-get install -y \
    postgresql-client

RUN ctags -R --fields=+l --languages=python --python-kinds=-iv -f ~/.tags $(python3 -c "import os, sys; print(' '.join('{}'.format(d) for d in sys.path if os.path.isdir(d)))")

RUN wget -O /wait-for-it.sh "https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh"
RUN chmod +x /wait-for-it.sh

CMD ["/wait-for-it.sh", "pgcikondb:5432", "--","tmuxinator"]

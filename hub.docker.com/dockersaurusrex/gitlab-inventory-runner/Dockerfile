FROM fedora:30
RUN dnf install -y python37 libpq-devel postgresql postgresql-devel python3-devel pipenv gcc git  
RUN dnf install -y libxcrypt-compat which
RUN pip3 install --user devpi-client 
RUN pip3 install --user kafka-python psycopg2
RUN pip3 install --user pipenv

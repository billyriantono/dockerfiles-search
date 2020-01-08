FROM middlefork/baseimage

# Make python3 the default
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1

# We can forego a Virtualenv in this container
#  --todo-- no, let's not. let's do it right. we may want python e.g. 3.7

# Install our python packages from requirements.txt.
# Let's be explicit and call it python-requirements.txt, here.
# Django, DRF, psycopg2, uwsgi, etc.
COPY python-requirements.txt /opt/python-requirements.txt
RUN python3 -m pip install --upgrade pip \
  && python3 -m pip install -r /opt/python-requirements.txt

# Start a new Django project, but rename its settings to 'settings_orig' so we can more easily customize.
WORKDIR /opt
RUN django-admin startproject drf \
  && mv drf/drf/settings.py drf/drf/settings_orig.py

# Now copy our customizations into the project
WORKDIR /opt/drf

COPY settings.py drf
COPY settings_rest.py drf
COPY urls.py drf

# Run our new Django project using uwsgi, expose it on native port 80
CMD uwsgi --http :80 --wsgi-file drf/wsgi.py









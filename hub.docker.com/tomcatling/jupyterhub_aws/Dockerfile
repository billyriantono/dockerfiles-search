# An incomplete base Docker image for running JupyterHub
#
# Add your configuration to create a complete derivative Docker image.
#
# Include your configuration settings by starting with one of two options:
#
# Option 1:
#
# FROM jupyterhub/jupyterhub:latest
#
# And put your configuration file jupyterhub_config.py in /srv/jupyterhub/jupyterhub_config.py.
#
# Option 2:
#
# Or you can create your jupyterhub config and database on the host machine, and mount it with:
#
# docker run -v $PWD:/srv/jupyterhub -t jupyterhub/jupyterhub
#
# NOTE
# If you base on jupyterhub/jupyterhub-onbuild
# your jupyterhub_config.py will be added automatically
# from your docker directory.

FROM jupyterhub/jupyterhub:latest

RUN PATH=$PATH:/usr/local/bin && pip install --no-cache-dir boto3

COPY jupyterhub_aws_spawner /opt/conda/lib/python3.6/site-packages/jupyterhub_aws_spawner

COPY minimal_authenticator/minimal_authenticator.py /opt/conda/lib/python3.6/site-packages/

COPY templates /srv/jupyterhub/templates

RUN mkdir -p /srv/jupyterhub/ && mkdir -p /etc/jupyterhub/
COPY jupyterhub_config.py /srv/jupyterhub/jupyterhub_config.py
COPY cull_idle_servers.py /srv/jupyterhub/cull_idle_servers.py

WORKDIR /srv/jupyterhub/

CMD ["jupyterhub"]

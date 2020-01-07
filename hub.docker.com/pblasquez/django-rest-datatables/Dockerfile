# Django, Django REST Framework, and Datatables (latest) on Python 3
# Copyright (C) 2019 Paul Blasquez <pblasquez@gmail.com>
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

FROM python:3

MAINTAINER Paul Blasquez <pblasquez@gmail.com>

RUN apt-get update && \
    pip install django && \
    pip install django-bootstrap4 && \
    pip install djangorestframework-datatables && \
    pip install django-rest-swagger && \
    pip install django-filter && \
    pip install django-composite-foreignkey && \
    pip install mysqlclient && \
    pip install markdown # Markdown support for the browsable API.

RUN mkdir /app

WORKDIR /app

EXPOSE 80

COPY docker-entrypoint.sh /

RUN chmod 755 /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

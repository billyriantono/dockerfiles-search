FROM aymazon/bi

CMD ["/sbin/my_init"]

RUN true \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt update \
    && apt-get install -y -q \
    gcc \
    && wget -q https://bitbucket.org/squeaky/portable-pypy/downloads/pypy-6.0.0-linux_x86_64-portable.tar.bz2 -O /tmp/pypy.tar.bz2 && tar xjf /tmp/pypy.tar.bz2 -C /opt/ \
    && cd /opt/pypy*/bin/ && ./pypy ./virtualenv-pypy /python-env \
    && source /python-env/bin/activate \
    && pip install -i https://pypi.douban.com/simple ipython==5.4.1 ipdb six pyrsistent fn toolz functoolsex pprofile pprofile_ext memory_profiler \
    && mkdir -p /root/.ipython/profile_default \
    && echo -e "c.InteractiveShellApp.exec_lines = [\n    '''from __future__ import absolute_import, division, print_function, unicode_literals''',\n\n    '''from functools import *''',\n    '''from operator import *''',\n    '''from itertools import *''',\n\n    '''from pyrsistent import *''',\n\n    '''from fn import F, _, _ as X''',\n    '''from fn.monad import Option, Full, Empty, optionable''',\n    '''from fn.op import apply, call, zipwith, foldl, foldr, unfold''',\n    '''from fn.stream import Stream''',\n    '''from fn.recur import tco''',\n    '''from fn.iters import padnone, ncycles, repeatfunc''',\n    '''from fn.iters import partition as splitin, splitat, splitby''',\n    '''from fn.iters import powerset, pairwise, iter_except, flatten''',\n\n    '''from toolz import *''',\n    '''from toolz.compatibility import *''',\n\n    '''from functoolsex import *''',\n\n    '''%autoreload 2''',\n]\nc.InteractiveShellApp.extensions = [\n    'autoreload',\n    'pprofile_ext',\n    'memory_profiler',\n]" > /root/.ipython/profile_default/ipython_config.py \
    && apt-get autoremove -y gcc \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

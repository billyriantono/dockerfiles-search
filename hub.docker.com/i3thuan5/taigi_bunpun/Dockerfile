FROM i3thuan5/hok8-bu7

# RUN pip install hue7jip8
RUN pip install --upgrade \
  https://github.com/i3thuan5/tai5-uan5_gian5-gi2_kang1-ku7/archive/master.zip \
  https://github.com/Taiwanese-Corpus/hue7jip8/archive/master.zip

RUN python manage.py 教典詞條
RUN python manage.py 教典例句

RUN python manage.py 詞彙分級
RUN python manage.py 台語數字
# RUN python manage.py itaigi

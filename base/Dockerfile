# Alpine Linux with webscraping phantomjs + selenium
#===================================================

FROM youske/alpine-conda:miniconda2
MAINTAINER youske miyakoshi <youske@gmail.com>

LABEL com.geeplus.description="alpine webscraping image" \
      com.geeplus.role="cache"

ENV LANG=ja_JP.UTF-8 \
    PYENV_HOME=/opt/pyenv

COPY requirements.txt /tmp/requirements.txt
COPY pyenv-virtual.conf /opt/pyenv-virtual.conf
RUN PACKAGES="phantomjs" && \
    DEPS="build-base musl-dev bison flex fontconfig-dev freetype-dev g++ gcc git gperf icu-dev libc-dev libjpeg-turbo-dev libpng-dev libx11-dev libxext-dev linux-headers make openssl-dev paxctl perl python ruby sqlite-dev" && \
    apk add --no-cache ${DEPS} -t buildpack && \
    pip install -U -r /tmp/requirements.txt && \
    git clone https://github.com/yyuu/pyenv.git ${PYENV_HOME} && \
    git clone https://github.com/yyuu/pyenv-virtualenv.git ${PYENV_HOME}/plugins/pyenv-virtualenv && \
    git clone git://github.com/ariya/phantomjs.git /opt/phantomjs && \
    apk del buildpack && rm -rf /tmp/* && rm -rf /var/cache/apk/*

ENTRYPOINT ["switch","shell=su admin -c /bin/bash","--","switch","root=/bin/bash","--","/init"]
CMD ["/bin/bash"]

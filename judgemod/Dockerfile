FROM python:3.7.7-alpine3.11

RUN addgroup -S judge

RUN adduser -D -u 1000 -G judge judge

WORKDIR /home/judge/judgeMod

RUN apk update && \
    apk add --no-cache --virtual \
    build-dependencies \
    build-base \
    libseccomp-dev \
    python3-dev \
    gcc \
    python2 \
    openjdk8 \
    openjdk9 \
    openjdk10 \
    openjdk11 \
    git \
    make \
    musl-dev \
    go \
    nodejs

# java 
RUN ln -s /usr/lib/jvm/java-1.8-openjdk/bin/java /usr/bin/java8
RUN ln -s /usr/lib/jvm/java-1.8-openjdk/bin/javac /usr/bin/javac8
RUN ln -s /usr/lib/jvm/java-9-openjdk/bin/java /usr/bin/java9
RUN ln -s /usr/lib/jvm/java-9-openjdk/bin/javac /usr/bin/javac9
RUN ln -s /usr/lib/jvm/java-10-openjdk/bin/java /usr/bin/java10
RUN ln -s /usr/lib/jvm/java-10-openjdk/bin/javac /usr/bin/javac10
RUN ln -s /usr/lib/jvm/java-11-openjdk/bin/java /usr/bin/java11
RUN ln -s /usr/lib/jvm/java-11-openjdk/bin/javac /usr/bin/javac11

# GoLang
RUN export PATH="/usr/local/go/bin:$PATH" \
    export GOPATH=/opt/go/ \
    export PATH=$PATH:$GOPATH/bin

RUN pip3 install cython

COPY --chown=judge:judge ./judgeMod /home/judge/judgeMod/

RUN python3 setup.py develop

USER judge

RUN mkdir /home/judge/judge_cache

RUN mkdir /home/judge/judge_log

RUN mkdir /home/judge/judge_sub_data

# RUN python3 ./test/all_lang_test.py

CMD ["python3", "sustoj/launch.py"]
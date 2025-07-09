FROM dmoj/runtimes-tier2

ARG TAG=master
ARG TIMEOUT=60

ENV BUILD_PACKAGES="recode" \
    RUNTIME_PACKAGES="" \
    JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk

RUN apt-get update && \
    apt-get install -y git

RUN apt-get install -y ${BUILD_PACKAGES} ${RUNTIME_PACKAGES} && \
    apt-get install -y vim && \
    curl -L https://github.com/igrigorik/vimgolf/raw/master/lib/vimgolf/lib/vimgolf/keylog.rb -o /root/keylog.rb && \
    echo '#!/bin/sh\n# Ref: shinhs anagol script\n# http://golf.shinh.org/version.rb\ncat - > /tmp/out\nTERM=dumb /usr/bin/vim -N -u NONE -i NONE -s "$1" /tmp/out > /dev/null 2>&1\ncat /tmp/out\nrm /tmp/out' > /usr/bin/vim && \
    chmod +x /usr/bin/vim && \
    curl -m $TIMEOUT "https://esolangs.org/wiki/Aubergine/aubergine.py" -L | awk -F "</?pre>" '{print $2}' RS="b\bb" | recode HTML..u8 > ~/aubergine.py && \
    echo '#!/bin/sh\ncat - | /usr/bin/python ~/aubergine.py "$1"' > /usr/bin/aubergine && \
    chmod +x /usr/bin/aubergine && \
    cd /tmp && \
    curl -m 30 "http://web.archive.org/web/20070423184121/http://www.harderweb.de/jix/langs/axo/axopp.0.1.0.cc" -LO && \
    sed -i 's/sranddev()/srand(time(NULL))/' axopp.0.1.0.cc && \
    g++ -O2 -Wall axopp.0.1.0.cc -o axopp -include stdlib.h && \
    mv axopp /usr/bin/axopp && \
    git clone --depth 1 https://github.com/GuyJoKing/Backhand.git ~/Backhand && \
    echo '#!bin/sh\ncat - | /usr/bin/python3 ~/Backhand/Backhand_Interpreter.py "$1"' > /usr/bin/backhand && \
    chmod +x /usr/bin/backhand && \
    apt-get purge -y --auto-remove ${BUILD_PACKAGES}

RUN mkdir /judge /problems && cd /judge && \
	curl -L https://github.com/cuminum/judge-server/archive/"${TAG}".tar.gz | tar -xz --strip-components=1 && \
    python3 -m venv --prompt=DMOJ /env && \
	/env/bin/pip3 install cython setuptools && \
	/env/bin/pip3 install -e . && \
	/env/bin/python3 setup.py develop && \
	HOME=~judge . ~judge/.profile && \
	runuser -u judge -w PATH -- /env/bin/dmoj-autoconf -V > /judge-runtime-paths.yml && \
	echo '  crt_x86_in_lib32: true' >> /judge-runtime-paths.yml

ENTRYPOINT ["/usr/bin/tini", "--", "/judge/.docker/entry"]
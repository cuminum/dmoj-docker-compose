FROM dmoj/runtimes-tier2

ARG TAG=master
ARG TIMEOUT=60

ENV BUILD_PACKAGES="cmake" \
    RUNTIME_PACKAGES=""

RUN apt-get update && \
    apt-get install -y git libtiff-dev libgdiplus erlang elixir gcc-12
RUN	apt-get install -y ${BUILD_PACKAGES} ${RUNTIME_PACKAGES} && \
	cd /tmp && \
    curl -m ${TIMEOUT} https://sourceforge.net/projects/cfunge/files/cfunge/0.9.0/cfunge-0.9.0.tar.bz2 -LO && \
    tar xjf cfunge-0.9.0.tar.bz2 && \
    cd cfunge-0.9.0 && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && \
    mv cfunge ~/cfunge && \
    apt-get purge -y --auto-remove ${BUILD_PACKAGES} && \
    rm -rf /var/cache/apk/* /tmp/*

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
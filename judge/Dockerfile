FROM dmoj/runtimes-tier2

ARG TAG=box-try
ARG TIMEOUT=60
ARG CACHE_BUST=unspecified

ENV BUILD_PACKAGES="cmake make" \
    RUNTIME_PACKAGES="libc6:i386 libncurses5:i386 libstdc++6:i386" \
	DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y git libtiff-dev libgdiplus erlang elixir gcc-12
RUN	curl -m ${TIMEOUT} https://gist.githubusercontent.com/tRue-math/3b54062756f31c1fa961f046c7ccd5d8/raw/cd4a765bf82fcf6a296c4c608fa0b14a6fbb38b9/fish.py -L -o /usr/bin/fish && \
    chmod +x /usr/bin/fish && \
    curl -m ${TIMEOUT} https://gist.githubusercontent.com/tRue-math/da6f9974456c1dbdea29a8e334ac6afb/raw/7533756e0c4622b809c4adbf4be5cdbb49579247/mao.py -L -o /usr/bin/mao && \
    chmod +x /usr/bin/mao && \
    runuser -u judge curl -m ${TIMEOUT} https://sh.rustup.rs -sSf | sh && \
    curl -m ${TIMEOUT} https://gist.githubusercontent.com/tRue-math/0265103969895f168612096eb783f7c0/raw/5112559a96433503960c160ffe1f295d6566e794/starry.rb -L -o /usr/bin/starry && \
    chmod +x /usr/bin/starry && \
    curl -m ${TIMEOUT} https://github.com/dnek/mines-esolang/archive/d5694877a24f6c37a9c84a848febc683baffddc2.zip -L -o /opt/mines.zip && \
    unzip /opt/mines.zip -d /opt/mines && \
    mv /opt/mines/mines-esolang-*/* /opt/mines && \
    rm -rf /opt/mines/mines-esolang-* && \
    echo '#!/bin/sh\nexec /usr/bin/python3 /opt/mines/mines/mines.py "$@"' > /usr/bin/mines && \
    chmod +x /usr/bin/mines && \
    curl -m ${TIMEOUT} https://gist.githubusercontent.com/tRue-math/95c2937888f106def8a96e37f76a73b9/raw/61c9876c1121886eaa7bff15fed60b73268018af/ferNANDo.py -L -o /usr/bin/fernando && \
    chmod +x /usr/bin/fernando && \
    cd /tmp && \
    git clone --depth 1 https://github.com/aheui/caheui.git && \
    cd caheui && make && mv aheui /usr/bin/aheui && \
    cd /tmp && \
    curl https://rdr.utopiat.net/files/mono//produire-mono-1.9.1182.tar.gz -LO && \
    mkdir -p /usr/lib/mono/produire && \
    tar xf produire-mono-1.9.1182.tar.gz -C /usr/lib/mono/produire && \
    echo '#!/bin/sh\nexec /usr/bin/mono /usr/lib/mono/produire/produire-mono/pconsole.exe "$@"' > /usr/bin/produire && \
    chmod +x /usr/bin/produire && \
    curl -m ${TIMEOUT} https://gist.githubusercontent.com/cuminum/2971133665df070915f47fe88a6418fd/raw/7c5eb6b1fe1f3f9f4b6fbe39edfe94780454a1bd/BF.py -L -o /usr/bin/bf-py && \
    /usr/bin/pip3 install --break-system-packages getch && \
    chmod +x /usr/bin/bf-py && \
    cd /opt && \
    git clone --depth 1 https://github.com/Adriandmen/05AB1E.git && \
    cd 05AB1E && (yes | PATH=/usr/bin:$PATH mix local.hex) && \
    PATH=/usr/bin:$PATH mix deps.get && \
    mix deps.update hackney && \
    (yes | PATH=/usr/bin:$PATH MIX_ENV=prod mix escript.build) && \
    echo '#!/bin/sh\nexec /usr/bin/escript /opt/05AB1E/osabie "$@"'>/usr/bin/05ab1e && \
    chmod +x /usr/bin/05ab1e && \
    dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y ${BUILD_PACKAGES} ${RUNTIME_PACKAGES} && \
    cd /tmp && \
    curl -m ${TIMEOUT} https://sourceforge.net/projects/cfunge/files/cfunge/0.9.0/cfunge-0.9.0.tar.bz2 -LO && \
    tar xjf cfunge-0.9.0.tar.bz2 && \
    cd cfunge-0.9.0 && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make && \
    mv cfunge /usr/bin/befunge98 && \
    apt-get install -y golang haskell-platform && \
    apt-get install -y nodejs pike8.0 php gnat algol68g gfortran && \
    apt-get install -y tcl expect && \
    mkdir /tmp/tcllib && \
    (curl -L https://github.com/tcltk/tcllib/archive/tcllib_1_18.tar.gz | tar -xz -C /tmp/tcllib --strip-components=1) && \
    tclsh /tmp/tcllib/installer.tcl -no-html -no-nroff -no-examples -no-gui -no-apps -no-wait -pkg-path /usr/lib/tcllib && \
    curl -L https://netcologne.dl.sourceforge.net/project/d-apt/files/d-apt.list -o /etc/apt/sources.list.d/d-apt.list && \
    apt-get update --allow-insecure-repositories && \
    apt-get -y --allow-unauthenticated install --reinstall d-apt-keyring && \
    apt-get update && \
    apt-get install -y tzdata && \
    apt-get install dmd-compiler dub -y && \
    apt-get autoremove -y && \
    git clone --depth 1 https://github.com/Adriandmen/2sable.git /usr/local/bin/2sable && \
    echo '#!/bin/sh\nexec /usr/bin/python3 /usr/local/bin/2sable/2sable.py "$@"' > /usr/bin/2sable && \
    chmod +x /usr/bin/2sable && \
    cd /tmp && \
    git clone --depth 1 https://github.com/olls/3var-interpreter.git && \
    cd 3var-interpreter && \
    make && \
    mv 3var /usr/bin/3var && \
	cd /tmp && \
    curl -m $TIMEOUT https://homepages.cwi.nl/~steven/abc/implementations/abc.tar.gz -LO && \
    tar xf abc.tar.gz -C ~ && \
	echo '#!/bin/sh\ninput=$(cat -)\n\nif [ -z "$input" ]; then\n  # At least one newline is required\n  echo '' | /root/ABC/abc "$1"\nelse\n  echo -n "$input" | /root/ABC/abc "$1"\nfi' > /usr/bin/abc && \
	chmod +x /usr/bin/abc && \
	cd /tmp && \
    curl -m $TIMEOUT https://github.com/graue/esofiles/raw/master/adjust/impl/adjust.18.1.tar.gz -LO && \
    tar xzf adjust.18.1.tar.gz && \
    cd adjust.18.1 && \
    gcc -O2 -Wall -o adjust adjust.c && \
    mv adjust /usr/bin/adjust && \
	git clone --depth 1 https://github.com/m-ender/alice.git /usr/local/bin/alice && \
	echo '#!/bin/sh\nexec /usr/bin/ruby /usr/local/bin/alice/interpreter.rb "$@"' > /usr/bin/alice && \
    chmod +x /usr/bin/alice && \
	cd /tmp && \
    git clone --depth 1 https://github.com/TryItOnline/alphabeta.git && \
    cd alphabeta && \
    make && \
    mv ab /usr/bin/alphabeta && \
	cd /tmp && \
    curl -m $TIMEOUT https://ftpmirror.gnu.org/gnu/apl/apl-1.8.tar.gz -LO && \
    tar xzf apl-1.8.tar.gz && \
    cd apl-1.8 && \
    ./configure && \
    (make -j5 CXX_WERROR= > /tmp/make.log) && \
    mv src/apl /usr/bin/apl && \
	cd /tmp && \
	git clone --depth 1 https://github.com/Nazek42/arcyou.git ~/arcyou && \
    sed -i 's/from collections import Hashable/from collections.abc import Hashable/' ~/arcyou/function.py && \
	echo '#!/bin/sh\n\ninfile=$(realpath "$1")\ncd ~/arcyou\n\ncat - | LANG=en_US.UTF8 /usr/bin/python3 arc.py "$infile"' > /usr/bin/arcyou && \
	chmod +x /usr/bin/arcyou && \
	git clone --depth 1 https://github.com/toyukan6/Arithmetic.git ~/Arithmetic && \
	echo '#!/bin/sh\n\ncat - | /usr/local/ruby-latest/bin/ruby ~/Arithmetic/eso.rb "$1"' > /usr/bin/arithmetic && \
	chmod +x /usr/bin/arithmetic && \
	curl -m $TIMEOUT http://lhartikk.github.io/ArnoldC.jar -o ~/ArnoldC.jar && \
	echo '#!/bin/sh\n\ninfile=$(realpath "$1")\nln -sf "$infile" /tmp/code.arnoidc\ncd /tmp\n/usr/bin/java -jar ~/ArnoldC.jar code.arnoidc\n\ncat - | /usr/bin/java code\n\nrm /tmp/code.arnoidc /tmp/code.class' > /usr/bin/arnoldc && \
	chmod +x /usr/bin/arnoldc && \
    apt-get purge -y --auto-remove ${BUILD_PACKAGES}

RUN mkdir /judge /problems && cd /judge && \
	curl -L "https://github.com/cuminum/judge-server/archive/${TAG}.tar.gz?cachebust=${CACHE_BUST}" | tar -xz --strip-components=1 && \
    python3 -m venv --prompt=DMOJ /env && \
	/env/bin/pip3 install cython setuptools && \
	/env/bin/pip3 install -e . && \
	/env/bin/python3 setup.py develop && \
	HOME=~judge . ~judge/.profile && \
	runuser -u judge -w PATH -- /env/bin/dmoj-autoconf -V > /judge-runtime-paths.yml && \
	echo '  crt_x86_in_lib32: true' >> /judge-runtime-paths.yml

ENTRYPOINT ["/usr/bin/tini", "--", "/judge/.docker/entry"]
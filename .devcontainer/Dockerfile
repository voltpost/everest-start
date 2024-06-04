# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/devcontainers/base:bookworm

ARG EVEREST_CMAKE_PATH=/usr/lib/cmake/everest-cmake
ENV CPM_SOURCE_CACHE=~/cache/CPM

# Configure system tools and install packages
RUN echo 'Acquire::http::Timeout "600";\nAcquire::ftp::Timeout "600";\nAcquire::Retries "10";' > /etc/apt/apt.conf.d/99timeout \
    && apt-get update \
    && apt-get install --no-install-recommends -y \
        # basic command line tools
        git \
        curl \
        rsync \
        # build tools
        ninja-build \
        make \
        cmake \
        # compilers
        binutils \
        gcc \
        g++ \
        # compiler tools
        clang-tidy \
        clangd \
        ccache \
        # development tools
        gdb \
        valgrind \
        # python3 support
        python3-pip \
        # required for testing
        libgtest-dev \
        lcov \
        # required by some everest libraries
        libboost-all-dev \
        libcap-dev \
        # required by libocpp
        libsqlite3-dev \
        libssl-dev \
        # required by everest-framework
        nodejs \
        libnode-dev \
        npm \
        # required by packet sniffer module
        pkg-config \
        libpcap-dev \
        # required by RiseV2G
        maven \
        # required by pybind11
        python3-dev \
        # required for certificate generation
        openssl \
        # required for cryptography
        libffi-dev \
        rust-all \
        # required by gcovr
        libxml2-dev \
        libxslt1-dev \
        # for simulated serial port
        socat \
    # clean up apt
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    # clean up existing Python install
    && rm -f /usr/lib/python3.11/EXTERNALLY-MANAGED \
    # install required Python packages
    && python3 -m pip install \
        environs>=9.5.0 \
        pydantic==1.* \
        psutil>=5.9.1 \
        cryptography>=3.4.6 \
        aiofile>=3.7.4 \
        py4j>=0.10.9.5 \
        netifaces>=0.11.0 \
        python-dateutil>=2.8.2 \
        gcovr==5.0 \
        # install ev-cli
        git+https://github.com/EVerest/everest-utils@v0.2.3#subdirectory=ev-dev-tools \
        # install everest-testing
        git+https://github.com/EVerest/everest-utils@v0.2.3#subdirectory=everest-testing \
        # install edm
        git+https://github.com/EVerest/everest-dev-environment@v0.6.1#subdirectory=dependency_manager \
    # install everest-cmake
    && git clone https://github.com/EVerest/everest-cmake.git $EVEREST_CMAKE_PATH \
    && ( \
        cd $EVEREST_CMAKE_PATH \
        && git checkout 329f8db \
        && rm -rf .git \
    )

ENV CMAKE_GENERATOR=Ninja \
    CMAKE_EXPORT_COMPILE_COMMANDS=ON

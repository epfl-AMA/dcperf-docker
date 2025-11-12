FROM quay.io/centos/centos:9

USER root

# --- System setup ---
RUN dnf install -y epel-release
RUN dnf install -y 'dnf-command(config-manager)'
RUN dnf config-manager --set-enabled crb

RUN dnf install -y --allowerasing \
  sudo \
  git \
  coreutils \
  diffutils \
  which \
  python \
  python3 \
  python3-click \
  python3-pyyaml \
  python3-tabulate \
  python3-pip \
  xz-devel \
  LibRaw-devel \
  libjpeg-turbo-devel \
  libpng-devel \
  ca-certificates \
  iputils \
  curl \
  wget

RUN pip3 install "numpy<2" pandas

WORKDIR /opt

RUN git clone https://github.com/facebookresearch/DCPerf.git dcperf && \
  cd dcperf && \
  git checkout 9308c3e3c404e0466f0a2929f15ddcf62b2215f6

WORKDIR /opt/dcperf

RUN curl -L --create-dirs https://mirrors.mit.edu/macports/distfiles/binutils/binutils-2.42.tar.xz \
  -o /opt/dcperf/benchmarks/tao_bench/build-folly/downloads/libiberty-binutils-2.42.tar.xz

RUN ./benchpress_cli.py install tao_bench_autoscale

RUN dnf install -y dmidecode \
  lshw \
  procps-ng

RUN dnf install -y numactl

CMD ["/bin/bash"]

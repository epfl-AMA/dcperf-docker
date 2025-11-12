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

# Use HTTPS for public repo
RUN git clone https://github.com/facebookresearch/DCPerf.git dcperf && \
  cd dcperf && \
  git checkout 9308c3e3c404e0466f0a2929f15ddcf62b2215f6

WORKDIR /opt/dcperf

RUN dnf install -y dmidecode

# Make sure CA certificates are active
# RUN update-ca-trust

# Add IPv4 preference + certs just before heavy network use, for extra safety
# RUN echo 'precedence ::ffff:0:0/96  100' >> /etc/gai.conf && update-ca-trust

# RUN ./benchpress_cli.py install tao_bench_autoscale

CMD ["bash"]

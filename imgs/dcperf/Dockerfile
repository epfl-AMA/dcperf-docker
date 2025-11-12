FROM ubuntu:22.04

USER root

RUN apt-get update && \
  apt-get install -y python3-pip git sudo && \
  pip3 install click pyyaml tabulate pandas

WORKDIR /opt/dcperf
COPY ../../external/dcperf .

RUN ./benchpress_cli.py install tao_bench_autoscale

CMD ["bash"]

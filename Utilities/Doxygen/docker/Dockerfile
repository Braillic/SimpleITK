FROM ubuntu:24.04 AS itk-doxygen
LABEL maintainer="Insight Software Consortium <community@itk.org>"

RUN apt-get update -y && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
  cmake \
  bison \
  build-essential \
  curl \
  flex \
  git \
  ninja-build \
  graphviz \
  python3 \
  python3-pip \
  python3-venv \
  perl \
  texlive-bibtex-extra &&\
  apt-get clean

RUN ln /usr/bin/dot /usr/sbin/dot

RUN git clone https://github.com/doxygen/doxygen.git && \
    ( cd doxygen && \
      git checkout Release_1_13_2 && \
      mkdir bld && cd bld && \
      cmake -G Ninja -DCMAKE_BUILD_TYPE=Release .. && \
      ninja install) && \
    rm -rf ./doxygen

RUN git config --global url."https://github.com/InsightSoftwareConsortium/".insteadOf "https://itk.org/"

COPY run.sh /tmp

#COPY patch /tmp/patch

WORKDIR /work

ENTRYPOINT ["/tmp/run.sh"]

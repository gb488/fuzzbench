# Copyright 2019 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder@sha256:87ca1e9e19235e731fac8de8d1892ebe8d55caf18e7aa131346fc582a2034fdd

# Note that we don't use the system libxml2 but a custom instrumented build.
# libgcrypt is required for the crypto extensions of libexslt.
# Need to build M4-1.4.19, autoconf-2.71, automake-1.16.3 manually in Ubuntu:20.
ENV M4_VERSION=1.4.19
ENV AUTOCONF_VERSION=2.71
ENV AUTOMAKE_VERSION=1.16.5
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    make \
    libtool \
    pkg-config \
    libgcrypt-dev && \
    wget https://ftp.gnu.org/gnu/m4/m4-$M4_VERSION.tar.gz && \
    tar xf m4-$M4_VERSION.tar.gz && \
    rm m4-$M4_VERSION.tar.gz && \
    ( \
        cd m4-$M4_VERSION/ && \
        ./configure && \
        make && \
        make install \
    ) && \
    wget https://ftp.gnu.org/gnu/autoconf/autoconf-$AUTOCONF_VERSION.tar.gz && \
    tar xf autoconf-$AUTOCONF_VERSION.tar.gz && \
    rm autoconf-$AUTOCONF_VERSION.tar.gz && \
    ( \
        cd autoconf-$AUTOCONF_VERSION/ && \
        ./configure && \
        make && \
        make install \
    ) && \
    wget https://ftp.gnu.org/gnu/automake/automake-$AUTOMAKE_VERSION.tar.gz && \
    tar xf automake-$AUTOMAKE_VERSION.tar.gz && \
    rm automake-$AUTOMAKE_VERSION.tar.gz && \
    ( \
        cd automake-$AUTOMAKE_VERSION && \
        ./configure && \
        make && \
        make install \
    )


RUN git clone https://gitlab.gnome.org/GNOME/libxml2.git && \
    git -C libxml2 checkout c7260a47f19e01f4f663b6a56fbdc2dafd8a6e7e && \
    git clone https://gitlab.gnome.org/GNOME/libxslt.git

ENV ACLOCAL_PATH='/usr/share/aclocal/'

WORKDIR libxslt
COPY build.sh $SRC/

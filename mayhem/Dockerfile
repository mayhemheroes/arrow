# Copyright 2020 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM --platform=linux/amd64 ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y -q && apt-get install -y -q --no-install-recommends \
    bison \
    build-essential \
    clang \
    cmake \
    flex \
    libgtest-dev \
    libgmock-dev \
    ninja-build \
    python3 \
    zip \
    && rm -rf /var/lib/apt/lists/*

COPY . /src/arrow

WORKDIR /work

ENV CC=clang
ENV CXX=clang++
ENV CFLAGS="-O1 -fno-omit-frame-pointer -DFUZZING_BUILD_MODE_UNSAFE_FOR_PRODUCTION -fsanitize=address -fsanitize-address-use-after-scope -fsanitize=fuzzer-no-link"
ENV CXXFLAGS="-O1 -fno-omit-frame-pointer -DFUZZING_BUILD_MODE_UNSAFE_FOR_PRODUCTION -fsanitize=address -fsanitize-address-use-after-scope -fsanitize=fuzzer-no-link"
ENV OUT=/out
ENV SRC=/src
ENV WORK=/work

COPY mayhem/build.sh /build.sh
RUN chmod +x /build.sh && mkdir -p /out && /build.sh

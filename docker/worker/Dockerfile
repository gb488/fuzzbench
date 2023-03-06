# Copyright 2020 Google LLC
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

FROM gcr.io/fuzzbench/base-image:latest@sha256:0f878820d6ae39d49aa939136121307854fbb2a88db9ae72dec8051badc93e16

ENV WORK /work
ENV SRC $WORK/src
RUN mkdir -p $SRC

ADD . $SRC/

ENTRYPOINT /bin/bash $SRC/docker/worker/startup-worker.sh
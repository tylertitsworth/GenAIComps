# Copyright (c) 2024 Intel Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM python:3.11-slim

ENV LANG C.UTF-8

RUN apt-get update -y && apt-get install -y --no-install-recommends --fix-missing \
    build-essential \
    libgl1-mesa-glx \
    libjemalloc-dev \
    vim

RUN useradd -m -s /bin/bash user && \
    mkdir -p /home/user && \
    chown -R user /home/user/

USER user

COPY comps /home/user/comps

RUN pip install --no-cache-dir --upgrade pip setuptools && \
    pip install --no-cache-dir -r /home/user/comps/dataprep/redis/requirements.txt

ENV PYTHONPATH=$PYTHONPATH:/home/user

USER root

RUN mkdir -p /home/user/comps/dataprep/redis/uploaded_files && chown -R user /home/user/comps/dataprep/redis/uploaded_files

USER user

WORKDIR /home/user/comps/dataprep/redis

ENTRYPOINT ["python", "prepare_doc_redis.py"]


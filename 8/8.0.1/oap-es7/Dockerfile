# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM apache/skywalking-base:8.0.1-es7 AS build

WORKDIR skywalking

RUN set -eux; \
    rm -rf "config/log4j2.xml"; \
    rm -rf "webapp"; rm -rf "agent";

COPY log4j2.xml config/
COPY docker-entrypoint.sh .
RUN mkdir ext-config; \
    mkdir ext-libs;

FROM openjdk:8-jre-alpine

ENV JAVA_OPTS=" -Xms256M "

LABEL maintainer="tanjian@apache.org"

COPY --from=build /skywalking /skywalking

WORKDIR skywalking

RUN apk add --no-cache \
    bash

EXPOSE 12800 11800 1234

ENTRYPOINT ["bash", "docker-entrypoint.sh"]

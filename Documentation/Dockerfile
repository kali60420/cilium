#FROM arm64v8/ubuntu:20.04
FROM docker.io/library/ubuntu:20.04

LABEL maintainer="maintainer@cilium.io"

ENV TZ=Europe/Kiev
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt update && apt-get install -y --no-install-recommends \
    aspell-en \
    nodejs \
    npm \
    bash \
    ca-certificates \
    enchant \
    git \
    python3-pip \
    python3 \
    python3-sphinx \
    && true

ADD ./requirements.txt /tmp/requirements.txt
RUN pip3 install -r /tmp/requirements.txt

ENV HOME=/tmp
ENV READTHEDOCS_VERSION=$READTHEDOCS_VERSION

## Workaround odd behaviour of sphinx versionwarning extension. It wants to
## write runtime data inside a system directory.
## We do rely on this extension, so we cannot just drop it.
RUN install -m 0777 -d /usr/local/lib/python3.7/site-packages/versionwarning/_static/data

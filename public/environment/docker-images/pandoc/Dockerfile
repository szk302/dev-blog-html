ARG ASCIIDOCTOR_VERSION='1.14.0'
ARG PANDOC_VERSION='2.17.0.1'

FROM pandoc/core:${PANDOC_VERSION} as pandoc

FROM asciidoctor/docker-asciidoctor:"${ASCIIDOCTOR_VERSION}"

ARG YQ_VERSION='4.16.1'

ENV YQ_TAR_FILE_URL="https://github.com/mikefarah/yq/releases/download/v${YQ_VERSION}/yq_linux_386.tar.gz"
ENV YQ_CHECKSUM_URL="https://github.com/mikefarah/yq/releases/download/v${YQ_VERSION}/checksums"

WORKDIR /tmp/work
SHELL ["/bin/ash", "-eo", "pipefail", "-c"]

COPY --from=pandoc \
  /usr/local/bin/pandoc \
  /usr/local/bin/

RUN apk --no-cache add \
        # pandocの依存モジュール
        gmp \
        libffi \
        lua5.3 \
        lua5.3-lpeg \
        # confulence投入に必要なモジュール
        coreutils \
        jq \
        sed
    # yqのインストール
RUN curl -LO "${YQ_TAR_FILE_URL}" && \
    curl -LO "${YQ_CHECKSUM_URL}" && \
    mkdir -p yq && \
    yq_tar_file_name="${YQ_TAR_FILE_URL##*/}" && \
    tar -zxvf ${yq_tar_file_name} && \
    mv ${yq_tar_file_name%%.tar.gz} /usr/bin/yq && \
    chmod +x /usr/bin/yq && \
    rm -rf /tmp/work/*

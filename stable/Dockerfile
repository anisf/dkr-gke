FROM google/cloud-sdk:alpine

ARG KUBECTL_VERSION="v1.19.0"
ARG HELM_VERSION="v3.7.1"
LABEL kubectl_version=${KUBECTL_VERSION}
LABEL helm_version=${HELM_VERSION}

RUN apk add --update ca-certificates bash \
    && apk add --no-cache --virtual .build-deps curl \
    && curl -L https://storage.googleapis.com/kubernetes-release/release/$KUBECTL_VERSION/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl  \
    && curl -LO https://get.helm.sh/helm-$HELM_VERSION-linux-amd64.tar.gz \
    && tar -zxvf helm-$HELM_VERSION-linux-amd64.tar.gz \
    && mv linux-amd64/helm /usr/local/bin/helm  \
    && apk del --purge .build-deps  \
    && rm -rf /var/cache/apk/* /tmp/* /root/.cache .build-deps linux-amd64 *.tar.gz \
    && adduser -S guser

USER guser
WORKDIR /home/guser

# Use C.UTF-8 locale to avoid issues with ASCII encoding
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

CMD [ "/bin/bash" ]
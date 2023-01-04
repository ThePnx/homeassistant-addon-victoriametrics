ARG BUILD_FROM
FROM $BUILD_FROM

ARG VM_VERSION

RUN /bin/bash -c 'set -ex && \
    ARCH=$(uname -m) && \
    if [ "$ARCH" == "x86_64" ]; then \
        wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/$VM_VERSION/victoria-metrics-linux-amd64-$VM_VERSION.tar.gz -qO- | tar xvz -C /; \
    elif [[ "$ARCH" == "arm"* ]]; then \
        wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/$VM_VERSION/victoria-metrics-linux-arm-$VM_VERSION.tar.gz -qO- | tar xvz -C /; \
    elif [ "$ARCH" == "aarch64" ]; then \
        wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/$VM_VERSION/victoria-metrics-linux-arm64-$VM_VERSION.tar.gz -qO- | tar xvz -C /; \
    else \
       echo "Unsupported architecture $ARCH"; \
       return -1; \
    fi'

# Copy data for add-on
COPY rootfs /
COPY prometheus.yml /
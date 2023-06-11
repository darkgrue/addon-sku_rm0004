ARG BUILD_FROM
FROM ${BUILD_FROM}

# Copy root filesystem
COPY rootfs /

# Setup base
RUN apk add --no-cache \
    procps \
 && apk add --no-cache --virtual .build-dependencies \
    build-base \
    git \
    linux-headers

RUN git clone https://github.com/darkgrue/SKU_RM0004 \
 && cd /SKU_RM0004 \
 && sed -i 's/\(#define CUSTOM_DISPLAY\) ".*"/\1 "Hass.io"/' .\hardware\rpiInfo\rpiInfo.h \
 && make \
 && cp display /usr/local/bin/ \
 && apk del .build-dependencies \
 && cd / \
 && rm -rf /SKU_RM0004

# Fix filesystem permissions
RUN chmod 0755 /etc/services.d/SKU_RM0004/finish \
 && chmod 0755 /etc/services.d/SKU_RM0004/run

RUN chown root /usr/local/bin \
 && chmod 0755 /usr/local/bin

RUN chown root /usr/local/bin/display \
 && chmod 0755 /usr/local/bin/display
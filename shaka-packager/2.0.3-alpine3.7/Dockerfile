FROM        alpine:3.7 as shaka-packager

ENV         VERSION 2.0.3
ENV         PATH=/depot_tools:$PATH

RUN         apk add --no-cache --virtual .build-deps \
                build-base \
                git \
                python \
                curl \
                bash \
                ninja && \
            git clone --depth 1 https://chromium.googlesource.com/chromium/tools/depot_tools.git

            # Get source
RUN         gclient config https://www.github.com/google/shaka-packager.git --name=src --unmanaged && \
            gclient sync --no-history -r v$VERSION && \
            mv src shaka-packager-$VERSION

RUN         cd shaka-packager-$VERSION && \
            ninja -C out/Release && \
            mv out/Release/packager /usr/local/bin/packager && \
            chmod +x /usr/local/bin/packager

###

FROM        alpine:3.7

ENTRYPOINT  ["packager"]

COPY        --from=shaka-packager /usr/local/bin/packager /usr/local/bin/packager

# buildkit bug workaround - https://github.com/moby/buildkit/issues/1368
FROM martinussuherman/alpine:3.13-amd64-glibc

ENV \
   # container/su-exec UID \
   EUID=1001 \
   # container/su-exec GID \
   EGID=1001 \
   # container/su-exec user name \
   EUSER=docker-user \
   # container/su-exec group name \
   EGROUP=docker-group \
   # container user home dir \
   EHOME= \
   # should user home dir get chown'ed? (yes/no) \
   ECHOWNHOME=no \
   # additional directories to create + chown (space separated) \
   ECHOWNDIRS= \
   # additional files to create + chown (space separated) \
   ECHOWNFILES= \
   # container timezone \
   TZ=UTC

RUN \
   apk --no-cache --update add \
   ca-certificates \
   \
   # .NET Core dependencies
   icu-libs \
   krb5-libs \
   libgcc \
   libintl \
   libssl1.1 \
   libstdc++ \
   lttng-ust \
   numactl \
   zlib

RUN \
   echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
   && apk update \
   && apk add --no-cache \
   libgdiplus \
   ttf-opensans

# Install ASP.NET Core
ENV ASPNET_VERSION=5.0.8

RUN \
   wget -O aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNET_VERSION/aspnetcore-runtime-$ASPNET_VERSION-linux-musl-x64.tar.gz \
   && aspnetcore_sha512='ea4d787e68fb4ab61448aa26894696192329d4e3a98ba9c95da588ec299523cca2d3b0a4e6ea35354b11cfd4ce9da594969806beb34cee249aac76dab46eb295' \
   && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
   && mkdir -p /usr/share/dotnet \
   && tar -oxzf aspnetcore.tar.gz -C /usr/share/dotnet \
   && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
   && rm aspnetcore.tar.gz

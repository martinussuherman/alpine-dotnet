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

RUN apk --no-cache --update add \
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

# Install ASP.NET Core
ENV ASPNET_VERSION=5.0.5

RUN wget -O aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNET_VERSION/aspnetcore-runtime-$ASPNET_VERSION-linux-musl-x64.tar.gz \
    && aspnetcore_sha512='04057353d890e73f5fe93cf9d05b2e84bf1f972a401acc631fc7ee7b83e97a4e40343458f274b7e900f96b94fbd2b954bde89b8874367776c82cb17567091d23' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -oxzf aspnetcore.tar.gz -C /usr/share/dotnet \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm aspnetcore.tar.gz

FROM martinussuherman/alpine-tz-ep:dev-glibc

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
ENV ASPNET_VERSION=3.1.11

RUN wget -O aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNET_VERSION/aspnetcore-runtime-$ASPNET_VERSION-linux-musl-x64.tar.gz \
    && aspnetcore_sha512='dfe6c191cbd87cf926a85da59095171df13c8bef8a5a8b7089c986475c4f3c508c66302ec008bee9ef458c2b2a5f9c348371139a2cddc3d9e0d74e879bc0f31a' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -oxzf aspnetcore.tar.gz -C /usr/share/dotnet \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm aspnetcore.tar.gz

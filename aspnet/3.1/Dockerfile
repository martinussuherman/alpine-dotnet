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

# Install ASP.NET Core
ENV ASPNET_VERSION=3.1.17

RUN \
   wget -O aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNET_VERSION/aspnetcore-runtime-$ASPNET_VERSION-linux-musl-x64.tar.gz \
   && aspnetcore_sha512='8861552d21a7efed982f31d228d42da7f8de8cb5343771de96034b3ddcabca2f9bc96bdadc40c7732c217bbc1b4d68999e91a98541076d6b5f535c2e6c9f8a4f' \
   && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
   && mkdir -p /usr/share/dotnet \
   && tar -oxzf aspnetcore.tar.gz -C /usr/share/dotnet \
   && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
   && rm aspnetcore.tar.gz

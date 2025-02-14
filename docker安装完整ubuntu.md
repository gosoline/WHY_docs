<!-- @format -->

# docker 安装完整 ubuntu

使用命令:

```shell
unminimize
```

因为不是每个 ubuntu 版本都有该脚本, 所以将该脚本贴出来供参考.

```shell
#!/bin/sh

set -e

echo "This system has been minimized by removing packages and content that are"
echo "not required on a system that users do not log into."
echo ""
echo "This script restores content and packages that are found on a default"
echo "Ubuntu server system in order to make this system more suitable for"
echo "interactive use."
echo ""
echo "Reinstallation of packages may fail due to changes to the system"
echo "configuration, the presence of third-party packages, or for other"
echo "reasons."
echo ""
echo "This operation may take some time."
echo ""
read -p "Would you like to continue? [y/N]" REPLY
echo    # (optional) move to a new line
if [ "$REPLY" != "y" ] && [ "$REPLY" != "Y" ]
then
    exit 1
fi

if [ -f /etc/dpkg/dpkg.cfg.d/excludes ] || [ -f /etc/dpkg/dpkg.cfg.d/excludes.dpkg-tmp ]; then
    echo "Re-enabling installation of all documentation in dpkg..."
    if [ -f /etc/dpkg/dpkg.cfg.d/excludes ]; then
        mv /etc/dpkg/dpkg.cfg.d/excludes /etc/dpkg/dpkg.cfg.d/excludes.dpkg-tmp
    fi
    echo "Updating package list and upgrading packages..."
    apt-get update
    # apt-get upgrade asks for confirmation before upgrading packages to let the user stop here
    apt-get upgrade
    echo "Restoring system documentation..."
    echo "Reinstalling packages with files in /usr/share/man/ ..."
    # Reinstallation takes place in two steps because a single dpkg --verified
    # command generates very long parameter list for "xargs dpkg -S" and may go
    # over ARG_MAX. Since many packages have man pages the second download
    # handles a much smaller amount of packages.
    dpkg -S /usr/share/man/ |sed 's|, |\n|g;s|: [^:]*$||' | DEBIAN_FRONTEND=noninteractive xargs apt-get install --reinstall -y
    echo "Reinstalling packages with system documentation in /usr/share/doc/ .."
    # This step processes the packages which still have missing documentation
    dpkg --verify --verify-format rpm | awk '/..5......   \/usr\/share\/doc/ {print $2}' | sed 's|/[^/]*$||' | sort |uniq \
         | xargs dpkg -S | sed 's|, |\n|g;s|: [^:]*$||' | uniq | DEBIAN_FRONTEND=noninteractive xargs apt-get install --reinstall -y
    if dpkg --verify --verify-format rpm | awk '/..5......   \/usr\/share\/doc/ {exit 1}'; then
        echo "Documentation has been restored successfully."
        rm /etc/dpkg/dpkg.cfg.d/excludes.dpkg-tmp
    else
        echo "There are still files missing from /usr/share/doc/:"
        dpkg --verify --verify-format rpm | awk '/..5......   \/usr\/share\/doc/ {print " " $2}'
        echo "You may want to try running this script again or you can remove"
        echo "/etc/dpkg/dpkg.cfg.d/excludes.dpkg-tmp and restore the files manually."
    fi
fi

if ! dpkg-query --show --showformat='${db:Status-Status}\n' ubuntu-minimal 2> /dev/null | grep -q '^installed$'; then
    echo "Installing ubuntu-minimal package to provide the familiar Ubuntu minimal system..."
    DEBIAN_FRONTEND=noninteractive apt-get install -y ubuntu-minimal ubuntu-standard
fi

if dpkg-query --show --showformat='${db:Status-Status}\n' ubuntu-server 2> /dev/null | grep -q '^installed$' \
   && ! dpkg-query --show --showformat='${db:Status-Status}\n' landscape-common 2> /dev/null | grep -q '^installed$'; then
    echo "Installing ubuntu-server recommends..."
    DEBIAN_FRONTEND=noninteractive apt-get install -y landscape-common
fi

# unminimization succeeded, there is no need to mention it in motd
rm -f /etc/update-motd.d/60-unminimize

```

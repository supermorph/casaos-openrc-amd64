# CasaOS OpenRC Package

## Overview
This package ports CasaOS v0.4.15 to OpenRC-based systems (Alpine Linux, Gentoo, Artix Linux, etc.).

## Features
- ✅ Native OpenRC init scripts (not sysvinit compatibility)
- ✅ Automatic dependency management
- ✅ All 6 CasaOS microservices included
- ✅ Complete web UI (39MB)
- ✅ Auto-start on boot
- ✅ Proper service ordering

## Package Files

1. **casaos-openrc_0.4.15.deb** (56MB) - For Debian-based systems with OpenRC
2. **casaos-openrc-0.4.15.tar.gz** (59MB) - Universal tarball for Alpine, Gentoo, etc.

## Package Contents
- 6 OpenRC init scripts in `/etc/init.d/`
- 6 CasaOS binaries in `/usr/bin/`
- Configuration files in `/etc/casaos/`
- Web UI in `/var/lib/casaos/www/`

## Services Included
1. casaos-message-bus - Inter-service communication
2. casaos-gateway - API gateway and web server
3. casaos-user-service - User authentication
4. casaos-local-storage - File management
5. casaos-app-management - Docker/app management
6. casaos - Main service

## Installation

### For Debian-based systems with OpenRC (Artix)
```bash
dpkg -i casaos-openrc_0.4.15.deb
```

### For Alpine Linux
```bash
# Extract tarball
cd / && tar xzf /path/to/casaos-openrc-0.4.15.tar.gz

# Make init scripts executable
chmod +x /etc/init.d/casaos*

# Add services to default runlevel
for svc in casaos-message-bus casaos-gateway casaos-user-service casaos-local-storage casaos-app-management casaos; do
    rc-update add $svc default
done

# Start services
for svc in casaos-message-bus casaos-gateway casaos-user-service casaos-local-storage casaos-app-management casaos; do
    rc-service $svc start
    sleep 2
done
```

### For Gentoo
```bash
# Extract to root
cd / && tar xzf /path/to/casaos-openrc-0.4.15.tar.gz

# Make init scripts executable
chmod +x /etc/init.d/casaos*

# Add to default runlevel
for svc in casaos-message-bus casaos-gateway casaos-user-service casaos-local-storage casaos-app-management casaos; do
    rc-update add $svc default
done

# Start services
rc-service casaos start  # Dependencies auto-start
```

Services auto-start after installation.

## Usage
```bash
# Start/stop services
rc-service casaos start
rc-service casaos stop
rc-service casaos restart
rc-service casaos status

# Enable/disable at boot (already done by package)
rc-update add casaos default
rc-update del casaos default

# View all CasaOS services
rc-status | grep casaos
```

## OpenRC Features
- `depend()` blocks define service dependencies
- OpenRC automatically handles start order
- `checkpath` creates runtime directories
- `command_background=true` for daemonization
- Automatic PID management

## Differences from SysVinit Version
- Uses OpenRC native syntax (not LSB headers)
- Simpler, cleaner init scripts
- Better dependency handling
- No manual dependency startup needed
- rc-update instead of update-rc.d

## Access
Web interface: http://localhost (or your server IP)

## Compatibility
- Alpine Linux
- Gentoo
- Artix Linux
- Any OpenRC-based distribution

Version Ported **Date:** 2 December 2025
Build Version: 0.4.15

## Maintainer Information

**Original Package Maintainer:** CasaOS Team <support@casaos.io>

**Maintainer of these ported packages:** Nobody really - these are just working proof of concepts. Well, I fixed it to work on sysvinit and ported that one to the other init systems.

Initially I just wanted CasaOS to work on Devuan Linux so I could make much more efficient bootable/installable images I can restore/install to my own home computers etc.

**PLEASE NOTE:** From the very first moment you ponder to try these, make a backup of the OS state and take it that **there's no responsibility of any description** because they were just for me and I am sharing for anyone to look at.

All original coding I didn't port belongs to the copyrighted maker/creator.

**P.S.** IceWhale/Zema: I didn't modify any API stuff so it uses your API as it was programmed originally, so please, don't sue - I'm just tryna make the proof of concept available for others to ponder.

**P.S.S.** I have help in parts with Claude AI, for the tricky sections. I'm no coder but I do know my way around a penguin-based OS heh.

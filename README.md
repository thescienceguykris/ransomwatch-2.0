# RansomWatch-2.0

<!-- [![Build Image](https://github.com/captainGeech42/ransomwatch/workflows/Build%20Image/badge.svg)](https://github.com/captainGeech42/ransomwatch/actions?query=workflow%3A%22Build+Image%22) [![Docker Hub Publish](https://github.com/captainGeech42/ransomwatch/workflows/Docker%20Hub%20Publish/badge.svg)](https://github.com/captainGeech42/ransomwatch/actions?query=workflow%3A%22Docker+Hub+Publish%22) [![Docker Hub Image](https://img.shields.io/docker/v/captaingeech/ransomwatch?color=blue)](https://hub.docker.com/repository/docker/captaingeech/ransomwatch/general) -->

RansomWatch is a ransomware leak site monitoring tool. It will scrape all of the entries on various ransomware leak sites, store the data in a SQLite database, and send notifications via Mattermost when a new victim shows up, or when a victim is removed.

The ambition is that future versions will automatically create a threat intelligence feed using the stix and taxii framework.

_Note: RansomWatch has been forked from the now unsupported RansomWatch project by [captainGeech42](https://github.com/captainGeech42/ransomwatch)._

## Configuration

In `config_vol/`, please copy `config.sample.yaml` to `config.yaml`, and add the following:

* Leak site URLs.
* Notification destinations. RansomWatch will support notifying via Mattermost.

Additionally, there are a few environment variables you may need to set:

* `RW_DB_PATH`: Path for the SQLite database to use
* `RW_CONFIG_PATH`: Path to the `config.yaml` file

These are both set in the provided `docker-compose.yml`.

## Usage

This is intended to be run in Docker via `docker-compose up -d`

```yml
version: "3"

services:
  app:
    name: ransomwatch-2.0
    depends_on:
      - proxy
    volumes:
      - ./db_vol:/db
      - ./config_vol:/config
    environment:
      PYTHONUNBUFFERED: 1
      RW_DB_PATH: /db/ransomwatch.db
      RW_CONFIG_PATH: /config/config.yaml

  proxy:
    image: captaingeech/tor-proxy:latest
```

## Leak Site Implementations

The following leak sites are supported:

- [x] Conti
- [X] Sodinokibi/REvil
- [X] Pysa
- [X] Avaddon
- [X] DarkSide
- [X] CL0P
- [X] Nefilim
- [X] Mount Locker
- [X] Suncrypt
- [x] Everest
- [X] Ragnarok
- [X] Ragnar_Locker
- [X] BABUK LOCKER
- [X] Pay2Key
- [X] Cuba
- [X] RansomEXX
- [X] Pay2Key
- [X] Ranzy Locker
- [X] Astro Team
- [X] BlackMatter
- [X] Arvin
- [X] El_Cometa
- [X] Lorenz
- [X] Xing
- [X] Lockbit
- [X] AvosLocker
- [X] LV
- [X] Marketo
- [X] Lockdata
- [X] Rook
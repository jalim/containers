<!---
NOTE: AUTO-GENERATED FILE
to edit this file, instead edit its template at: ./github/scripts/templates/README.md.j2
-->
<div align="center">


## Containers

_An opinionated collection of container images_

</div>

<div align="center">

![GitHub Repo stars](https://img.shields.io/github/stars/jalim/containers?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/jalim/containers?style=for-the-badge)
![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/jalim/containers/release-scheduled.yaml?style=for-the-badge&label=Scheduled%20Release)

</div>

Welcome to my container images, if looking for a container start by [browsing the GitHub Packages page for this repo's packages](https://github.com/jalim?tab=packages&repo_name=containers).

## Mission statement

The goal of this project is to support [semantically versioned](https://semver.org/), [rootless](https://rootlesscontaine.rs/), and [multiple architecture](https://www.docker.com/blog/multi-arch-build-and-images-the-simple-way/) containers for various applications.

It also adheres to a [KISS principle](https://en.wikipedia.org/wiki/KISS_principle), logging to stdout, [one process per container](https://testdriven.io/tips/59de3279-4a2d-4556-9cd0-b444249ed31e/), no [s6-overlay](https://github.com/just-containers/s6-overlay) and all images are built on top of [Alpine](https://hub.docker.com/_/alpine) or [Ubuntu](https://hub.docker.com/_/ubuntu).

## Tag immutability

The containers built here do not use immutable tags, as least not in the more common way you have seen from [linuxserver.io](https://fleet.linuxserver.io/) or [Bitnami](https://bitnami.com/stacks/containers).

We do take a similar approach but instead of appending a `-ls69` or `-r420` prefix to the tag we instead insist on pinning to the sha256 digest of the image, while this is not as pretty it is just as functional in making the images immutable.

| Container                                          | Immutable |
|----------------------------------------------------|-----------|
| `ghcr.io/jalim/sonarr:rolling`                   | ❌         |
| `ghcr.io/jalim/sonarr:3.0.8.1507`                | ❌         |
| `ghcr.io/jalim/sonarr:rolling@sha256:8053...`    | ✅         |
| `ghcr.io/jalim/sonarr:3.0.8.1507@sha256:8053...` | ✅         |

_If pinning an image to the sha256 digest, tools like [Renovate](https://github.com/renovatebot/renovate) support updating the container on a digest or application version change._

## Rootless

To run these containers as non-root make sure you update your configuration to the user and group you want.

### Docker compose

```yaml
networks:
  sonarr:
    name: sonarr
    external: true
services:
  sonarr:
    image: ghcr.io/jalim/sonarr:3.0.8.1507
    container_name: sonarr
    user: 65534:65534
    # ...
```

### Kubernetes

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sonarr
# ...
spec:
  # ...
  template:
    # ...
    spec:
      # ...
      securityContext:
        runAsUser: 65534
        runAsGroup: 65534
        fsGroup: 65534
        fsGroupChangePolicy: OnRootMismatch
# ...
```

## Passing arguments to a application

Some applications do not support defining configuration via environment variables and instead only allow certain config to be set in the command line arguments for the app. To circumvent this, for applications that have an `entrypoint.sh` read below.

1. First read the Kubernetes docs on [defining command and arguments for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/).
2. Look up the documentation for the application and find a argument you would like to set.
3. Set the argument in the `args` section, be sure to include `entrypoint.sh` as the first arg and any application specific arguments thereafter.

    ```yaml
    args:
      - /entrypoint.sh
      - --port
      - "8080"
    ```

## Configuration volume

For applications that need to have persistent configuration data the config volume is hardcoded to `/config` inside the container. This is not able to be changed in most cases.

## Available Images

Each Image will be built with a `rolling` tag, along with tags specific to it's version. Available Images Below

Container | Channel | Image
--- | --- | ---
[actions-runner](https://github.com/jalim/containers/pkgs/container/actions-runner) | stable | ghcr.io/jalim/actions-runner
[bazarr](https://github.com/jalim/containers/pkgs/container/bazarr) | stable | ghcr.io/jalim/bazarr
[home-assistant](https://github.com/jalim/containers/pkgs/container/home-assistant) | stable | ghcr.io/jalim/home-assistant
[jbops](https://github.com/jalim/containers/pkgs/container/jbops) | stable | ghcr.io/jalim/jbops
[lidarr](https://github.com/jalim/containers/pkgs/container/lidarr) | master | ghcr.io/jalim/lidarr
[lidarr-develop](https://github.com/jalim/containers/pkgs/container/lidarr-develop) | develop | ghcr.io/jalim/lidarr-develop
[lidarr-nightly](https://github.com/jalim/containers/pkgs/container/lidarr-nightly) | nightly | ghcr.io/jalim/lidarr-nightly
[par2cmdline-turbo](https://github.com/jalim/containers/pkgs/container/par2cmdline-turbo) | stable | ghcr.io/jalim/par2cmdline-turbo
[plex](https://github.com/jalim/containers/pkgs/container/plex) | stable | ghcr.io/jalim/plex
[plex-beta](https://github.com/jalim/containers/pkgs/container/plex-beta) | beta | ghcr.io/jalim/plex-beta
[postgres-init](https://github.com/jalim/containers/pkgs/container/postgres-init) | stable | ghcr.io/jalim/postgres-init
[prowlarr](https://github.com/jalim/containers/pkgs/container/prowlarr) | master | ghcr.io/jalim/prowlarr
[prowlarr-develop](https://github.com/jalim/containers/pkgs/container/prowlarr-develop) | develop | ghcr.io/jalim/prowlarr-develop
[prowlarr-nightly](https://github.com/jalim/containers/pkgs/container/prowlarr-nightly) | nightly | ghcr.io/jalim/prowlarr-nightly
[qbittorrent](https://github.com/jalim/containers/pkgs/container/qbittorrent) | stable | ghcr.io/jalim/qbittorrent
[qbittorrent-beta](https://github.com/jalim/containers/pkgs/container/qbittorrent-beta) | beta | ghcr.io/jalim/qbittorrent-beta
[radarr](https://github.com/jalim/containers/pkgs/container/radarr) | master | ghcr.io/jalim/radarr
[radarr-develop](https://github.com/jalim/containers/pkgs/container/radarr-develop) | develop | ghcr.io/jalim/radarr-develop
[radarr-nightly](https://github.com/jalim/containers/pkgs/container/radarr-nightly) | nightly | ghcr.io/jalim/radarr-nightly
[readarr-develop](https://github.com/jalim/containers/pkgs/container/readarr-develop) | develop | ghcr.io/jalim/readarr-develop
[readarr-nightly](https://github.com/jalim/containers/pkgs/container/readarr-nightly) | nightly | ghcr.io/jalim/readarr-nightly
[sabnzbd](https://github.com/jalim/containers/pkgs/container/sabnzbd) | stable | ghcr.io/jalim/sabnzbd
[sonarr](https://github.com/jalim/containers/pkgs/container/sonarr) | main | ghcr.io/jalim/sonarr
[sonarr-develop](https://github.com/jalim/containers/pkgs/container/sonarr-develop) | develop | ghcr.io/jalim/sonarr-develop
[theme-park](https://github.com/jalim/containers/pkgs/container/theme-park) | stable | ghcr.io/jalim/theme-park
[volsync](https://github.com/jalim/containers/pkgs/container/volsync) | stable | ghcr.io/jalim/volsync


## Deprecations

Containers here can be **deprecated** at any point, this could be for any reason described below.

1. The upstream application is **no longer actively developed**
2. The upstream application has an **official upstream container** that follows closely to the mission statement described here
3. The upstream application has been **replaced with a better alternative**
4. The **maintenance burden** of keeping the container here **is too bothersome**

**Note**: Deprecated containers will remained published to this repo for 6 months after which they will be pruned.

## Credits

A lot of inspiration and ideas are thanks to the hard work of [hotio.dev](https://hotio.dev/) and [linuxserver.io](https://www.linuxserver.io/) contributors.

# Changelog

All notable changes to this project are documented here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). The project has no version of its own —
the images are tagged with the Java version they contain — so every entry is headed by the date it reached `main`.
That date is also its git tag, with a release on GitHub.

## 2026-11-03

### Security
- Java `17.0.21`, `21.0.13` and `25.0.5`, the OpenJDK security releases of October 2026 (were `17.0.20`, `21.0.12` and
  `25.0.4`). Alpine `3.24` replaced the pinned packages on 2026-10-31, so the weekly build of 2026-11-01 failed for these
  three versions and their images stayed on the previous release. The Debian pair moves to `25.0.5+8`
- Base images raised for all four Java versions: `alpine:3.24.3` (was `3.24.2`) and `docker:29.9.2-dind` (was
  `29.9.1-dind`, now on Alpine `3.24.3` as well). Java 11 stays at `11.0.32`, the newest release Alpine packages

## 2026-10-19

### Added
- A git tag and a GitHub release for every entry of this changelog, named after its date

## 2026-10-18

### Security
- The packages of the base image are upgraded in every current image (`apk --no-cache upgrade`, `apt-get upgrade`).
  The exactly pinned base images had kept them at their release state, so the images still held OpenSSL `3.5.8`
  although Alpine `3.24` already offered `3.5.9`, a security release whose most severe fix is rated High - plus the
  pending fixes for zlib, the X11 libraries, curl, expat and xz; the Debian images missed 13 updates, among them libc6
- Base images raised: `alpine:3.24.2` (was `3.24.1`), `docker:29.9.1-dind` (was `29.7.2-dind`, now on Alpine
  `3.24.2` as well) and `debian:13.7-slim` (was `13.6-slim`). The Java versions stay
- The pipeline takes its tokens over stdin and through the environment instead of the command line

### Changed
- README Dockerfile example: `exec java`, so the JVM receives `SIGTERM` as process 1; heap at 75 % of the container
  limit; non-root `USER`; `UTC`. Options current JDKs no longer need are gone, each with a note
- README GitLab CI example: pushes to `$CI_REGISTRY_IMAGE` and logs in with `--password-stdin`
- The short description is the same text on Docker Hub, GitLab and GitHub

### Removed
- `rm -rf /var/cache/apk/*` from the current Alpine Dockerfiles — `apk --no-cache` leaves no cache behind

## 2026-10-13

### Added
- Mirror on [GitHub](https://github.com/epicsoft-llc/openjdk); the README names GitLab as the source and GitHub as
  the mirror
- README section on development: repository layout, CI, adding a Java patch release, checking a change locally
- `CHANGELOG.md`, `AGENTS.md`, `.gitignore` and `.gitattributes`, which keeps line endings at LF

### Changed
- Docker Hub short description names the Java versions, distributions and platforms

## 2026-09-06

### Added
- Debian headless JDK and JRE images for Java 25 on `debian:13.6-slim`, for native libraries that need glibc:
  `jdk25.0.4-debian-headless`, `jre25.0.4-debian-headless` and their floating tags
- All images are published as multi-platform manifests for `linux/amd64` and `linux/arm64`

### Changed
- Floating tags are copied inside the registry (`docker buildx imagetools create`) instead of pull, tag and push,
  which would reduce them to a single platform

## 2026-09-01

### Changed
- Release jobs run on the default branch only; builds on other branches push exact-version tags only

### Fixed
- The `org.label-schema.vcs-url` label pointed to the `master` branch instead of `main`

## 2026-08-16

### Added
- Java 11.0.32, 17.0.20, 21.0.12 and 25.0.4 — JDK on `docker:29.7.2-dind`, JRE on `alpine:3.24.1`

## 2026-08-02

### Fixed
- Pushing the images: they are built without provenance and SBOM attestations (`BUILDX_NO_DEFAULT_ATTESTATIONS`)

## 2026-05-24

### Added
- Java 11.0.31, 17.0.19, 21.0.11 and 25.0.3 — JDK on `docker:29.5.2-dind`, JRE on `alpine:3.23.4`

## 2026-05-15

### Added
- Java 25.0.2 — JDK on `docker:29.4.3-dind`, JRE on `alpine:3.23.4`

### Changed
- `jdk`, `jre` and `latest` point to Java 25 instead of Java 21

## 2026-02-20

### Added
- Java 11.0.30, 17.0.18 and 21.0.10 — JDK on `docker:29.2.1-dind`, JRE on `alpine:3.23.3`

## 2025-11-16

### Added
- Java 11.0.29, 17.0.17 and 21.0.9 — JDK on `docker:29.0.1-dind`, JRE on `alpine:3.22.2`

## 2025-10-05

### Changed
- The Docker Hub description is uploaded with `peterevans/dockerhub-description:4` instead of `:latest`

## 2025-07-20

### Added
- Java 11.0.28, 17.0.16 and 21.0.8 — JDK on `docker:28.3.2-dind`, JRE on `alpine:3.22.1`

## 2025-04-20

### Added
- Java 11.0.27, 17.0.15 and 21.0.7 — JDK on `docker:28.1.1-dind`, JRE on `alpine:3.21.3`

## 2025-02-16

### Added
- Java 11.0.26, 17.0.14 and 21.0.6 — JDK on `docker:27.5.1-dind`, JRE on `alpine:3.21.3`

## 2024-10-27

### Added
- Java 11.0.25, 17.0.13 and 21.0.5 — JDK on `docker:27.3.1-dind`, JRE on `alpine:3.20.3`

## 2024-07-18

### Added
- Java 11.0.24, 17.0.12 and 21.0.4 — JDK on `docker:27.0.3-dind`, JRE on `alpine:3.20.1`

## 2024-04-30

### Added
- Java 11.0.23, 17.0.11 and 21.0.3 — JDK on `docker:26.1.0-dind`, JRE on `alpine:3.19.1`

## 2024-02-18

### Changed
- Base images of the current versions raised to `docker:25.0.3-dind` and `alpine:3.19.1`

### Fixed
- `latest` was set by the Java 17 and the Java 21 release job; it now comes from one job, from Java 21

## 2024-01-25

### Added
- Java 21.0.2; `jdk` and `jre` point to Java 21
- Java 11.0.22 and 17.0.10 — all three JDKs on `docker:25.0.1-dind`, JREs on `alpine:3.19.0`

### Changed
- The Java packages are pinned to their exact Alpine package revision

## 2023-11-18

### Added
- Java 11.0.21 and 17.0.9 — JDK on `docker:24.0.7-dind`, JRE on `alpine:3.18.4`

## 2023-09-07

### Added
- Java 11.0.20 and 17.0.8 — JDK on `docker:24.0.6-dind`, JRE on `alpine:3.18.3`

## 2023-06-20

### Added
- Java 11.0.19 and 17.0.7 — JDK on `docker:24.0.2-dind`, JRE on `alpine:3.18.2`

## 2023-02-11

### Added
- First images: Java 11.0.18 and 17.0.6 — JDK on `docker:23.0.1-dind`, JRE on `alpine:3.17.2`

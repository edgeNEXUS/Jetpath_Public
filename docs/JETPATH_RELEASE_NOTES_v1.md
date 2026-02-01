# Jetpath v1.0.0 Release Notes

Release date: 2026-01-30

## Overview
Jetpath v1.0.0 delivers an eBPF/XDP load-balancing and routing data plane with
a unified JSON + REST control plane. It supports HTTP/1.x L7 parsing (bounded),
cookie persistence (proxy mode), and debug observability via a BPF ring buffer.

## Highlights
- L4 load balancing: round robin, weighted RR, least connection (approx),
  source persistence, cookie persistence (HTTP/1.x).
- L4 routing: exact IPv4 src/dst match.
- Defend drop list in XDP.
- NAT/DSR forwarding (proxy + gateway/DSR).
- L7 HTTP parsing: host/path extraction and routing (bounded).
- Debug logging levels with ring buffer events and verbose HTTP strings.
- Docker packaging for deployment.

## Packaging
- Docker image build: `docker/jetpath/Dockerfile`
- Docker compose example: `docker/jetpath/docker-compose.yml`

## Known limitations
- HTTPS is not parsed (TLS encrypted).
- IPv6 data plane not implemented.
- Route ranges are not enforced in XDP.
- Cookie persistence works only in proxy mode.
- L7 parsing assumes headers arrive in the first 1–2 packets.

## Documentation
- Spec: `docs/JETNEXUS_EBPF_SPEC.md`
- User guide: `docs/JETNEXUS_USER_GUIDE.md`
- Docker deployment: `docs/JETPATH_DOCKER_DEPLOYMENT.md`
- OpenAPI: `docs/jetnexus_openapi.yaml`
- Test plan: `docs/TEST_PLAN.md`


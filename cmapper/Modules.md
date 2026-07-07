# CMapper Modules

CMapper is built around independent collectors responsible for discovering, enriching, or updating specific types of infrastructure information.

Each collector can run repeatedly on a defined interval. This allows CMapper to refresh different parts of the infrastructure model at different speeds instead of relying only on one full discovery cycle.

## Design Principles

- Independent collector execution
- Queue-driven scheduling
- Repeated interval-based execution
- Vendor-specific discovery
- JSON-based output to the CMapper server
- Extensible collector model

## Current Collectors

### MikroTik MAC Discovery

Discovers devices and MAC information from MikroTik infrastructure.

### OUI Table Update

Updates the OUI database used to identify device vendors from MAC addresses.

### DNS Domain Lookup

Performs DNS-based hostname/domain lookup to enrich discovered infrastructure data.

### Cisco CDP Discovery

Uses Cisco Discovery Protocol to discover neighboring infrastructure devices and topology relationships.

### Ubiquiti CDP Packet Capture

Captures Ubiquiti CDP/discovery packets to identify Ubiquiti network devices and enrich topology information.

### Uniview NVR CDP Packet Capture

Captures Uniview NVR discovery/CDP-style packets to identify surveillance infrastructure and related network presence.

### DHCP Lease Table Lookup

Reads DHCP lease information to associate IP addresses, MAC addresses, and device identity data.

## Collector Output

Collectors send their results to the CMapper server using JSON-formatted data.

This separates collection from interpretation:

- Collectors discover information.
- The server receives structured JSON.
- CMapper updates inventory, topology, and related infrastructure data.

## Scheduling Philosophy

CMapper modules are not treated as one monolithic scan.

Each collector can be looped and scheduled based on how often that data needs to be refreshed. Fast-changing data can be collected more frequently, while slower-changing discovery can run less often.

This keeps infrastructure visibility updated while avoiding unnecessary load.
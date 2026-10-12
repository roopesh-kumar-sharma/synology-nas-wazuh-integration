# Synology NAS Integration with Wazuh

**Centralized logging, authentication monitoring, and security event visualization for Synology DSM.**

This project documents a lab implementation of integrating a Synology NAS with Wazuh. It covers syslog forwarding, centralized log collection, archive indexing, custom authentication decoders, detection rules, and dashboard creation.

The goal is to provide a practical, reproducible reference for system administrators who want to monitor Synology NAS activity using Wazuh.

> **Project status:** Work in progress. The documentation and configuration examples are being refined and validated.

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Lab Environment](#lab-environment)
- [Features](#features)
- [Documentation](#documentation)
- [Repository Structure](#repository-structure)
- [Implementation Summary](#implementation-summary)
- [Security Considerations](#security-considerations)
- [Limitations](#limitations)
- [References](#references)

## Overview

Synology DSM provides system and authentication logs that can be forwarded to a centralized monitoring platform.

In this implementation, the NAS forwards logs to a Wazuh manager over TCP syslog. Wazuh archives the incoming events, while custom decoders and rules are used to identify selected DSM authentication events.

The resulting alerts can be explored and visualized through the Wazuh Dashboard.

## Architecture

```text
+---------------------+
|   Synology NAS      |
|   Synology DSM      |
|   Log Center        |
+----------+----------+
           |
           | Syslog over TCP :514
           v
+---------------------+
|    Wazuh Manager    |
|                     |
|  Log Collection     |
|  Archive Logging    |
|  Custom Decoders    |
|  Detection Rules    |
+----------+----------+
           |
           v
+---------------------+
|  Wazuh Dashboard    |
|                     |
|  Event Exploration  |
|  Authentication     |
|  Alerts & Charts    |
+---------------------+
```

## Lab Environment

| Component | Configuration |
|---|---|
| SIEM and analysis | Wazuh 4.14.4 |
| NAS | Synology DS423Plus |
| Operating environment | Synology DSM |
| Log transport | TCP syslog |
| Syslog port | 514 |
| Log analysis | Custom Wazuh decoders and rules |
| Visualization | Wazuh Dashboard |

Configuration details may differ across DSM and Wazuh versions.

## Features

- Centralized collection of Synology DSM logs
- TCP syslog forwarding from Synology Log Center
- Wazuh archive logging and index verification
- Custom decoding of selected authentication events
- Detection rules for successful and failed DSM logins
- Validation using Wazuh's log testing utility
- Dashboard visualizations for authentication events

## Documentation

### Part 1: Centralized Log Monitoring

Covers syslog configuration, network verification, Wazuh archive logging, index discovery, and event visualization.

**Guide:** [Part 1: Centralized Logging](https://medium.com/@rupesharma203/integrating-synology-nas-with-wazuh-for-centralized-log-monitoring-and-visualization-0f82e7180d63)

### Part 2: Authentication Event Monitoring

Covers custom decoders, detection rules, decoder testing, live alert verification, and dashboard creation.

**Guide:** [Part 2: Authentication Monitoring](https://medium.com/@rupesharma203/monitoring-synology-nas-authentication-events-with-wazuh-custom-decoders-rules-and-dashboards-dfea97a01604)

## Repository Structure

```text
synology-wazuh-integration/
├── README.md
├── docs/
│   ├── part-1-centralized-logging.md
│   └── part-2-authentication-monitoring.md
├── decoders/
│   └── synology_decoders.xml
├── rules/
│   └── synology_rules.xml
└── screenshots/
```

## Implementation Summary

The integration is divided into two stages.

**Stage 1: Log collection**

Synology Log Center forwards events to the Wazuh manager. Network traffic and archived events are checked to confirm that logs are arriving and being indexed.

**Stage 2: Authentication monitoring**

Custom decoders extract selected authentication fields from DSM log messages. Custom rules classify matching events as successful or failed authentication events. Live alerts are then verified before building visualizations.

## Security Considerations

- Restrict the syslog listener to trusted senders.
- Use a protected network for log transport, or an appropriately secured transport when logs cross untrusted networks.
- Sanitize configuration examples and screenshots before publication.
- Never publish credentials, API keys, private keys, or sensitive production logs.
- Check custom rule IDs for conflicts before deploying them.
- Test configuration changes in a controlled environment before production use.

## Limitations

The example authentication rules cover selected DSM login events only.

They do not automatically detect every brute-force campaign, block source IP addresses, or provide comprehensive monitoring of all Synology administrative activities.

Additional decoders, rules, correlation logic, and response integrations may be needed for broader detection coverage.

## References

- [Wazuh Documentation](https://documentation.wazuh.com/current/)
- [Custom Wazuh Decoders](https://documentation.wazuh.com/current/user-manual/ruleset/decoders/custom.html)
- [Testing Wazuh Rules and Decoders](https://documentation.wazuh.com/current/user-manual/ruleset/testing.html)
- [Wazuh Rules](https://documentation.wazuh.com/current/user-manual/ruleset/rules.html)
- [Synology Log Center](https://kb.synology.com/en-us/DSM/help/LogCenter)

## Author

Rupesh Kumar Sharma

Linux System Administrator | Wazuh Ambassador

This repository is intended for technical learning and demonstration. Verify the configuration against your own environment before applying it to production systems.

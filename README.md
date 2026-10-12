# Synology NAS Integration with Wazuh

A practical guide to integrating a Synology NAS with Wazuh for centralized log collection, authentication monitoring, and security event visualization.

## Overview

This project documents my lab implementation of forwarding Synology DSM logs to a Wazuh manager using TCP syslog. It also covers custom decoders and rules for identifying successful and failed DSM authentication events.

## Lab Environment

- **SIEM:** Wazuh 4.14.4
- **NAS:** Synology DS423Plus
- **Log transport:** Syslog over TCP, port 514
- **Log analysis:** Wazuh custom decoders and rules
- **Visualization:** Wazuh Dashboard

Versions and configurations may need adjustment for other environments.

## Tutorials

### Part 1: Centralized Log Monitoring

Covers syslog forwarding, listener configuration, archive logging, index verification, and log visualization.

[Read Part 1](docs/part-1-centralized-logging.md)

### Part 2: Authentication Monitoring

Covers custom decoders, detection rules, testing, live alert verification, and authentication dashboards.

[Read Part 2](docs/part-2-authentication-monitoring.md)

## Configuration Files

- `decoders/synology_decoders.xml`: Custom decoders for DSM login events.
- `rules/synology_rules.xml`: Example rules for successful and failed authentication events.

Review the files and adapt them to your environment before deployment.

## Limitations

The example rules detect individual successful and failed login events. They do not, by themselves, detect every brute-force campaign, block source IP addresses, or cover all Synology DSM event categories.

## Author

Rupesh Kumar Sharma

Linux System Administrator | Wazuh Ambassador

## Disclaimer

This is a lab-based technical learning project. Test all configurations in a controlled environment before applying them to production systems.

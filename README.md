# Enterprise Hybrid-Cloud Home Laboratory

## Executive Summary

This repository houses the architectural designs, network configurations, and security policies of a multi-VLAN, enterprise-grade home laboratory. Rather than relying on consumer-grade hardware and flat networking topologies, this environment is architected to mirror a resilient corporate infrastructure. It serves as a continuous deployment and testing ground for advanced network engineering, automated security monitoring (SIEM), and containerized AI-driven operations.

## Engineering Objectives

* **Network Segmentation:** Enforce strict zero-trust communication boundaries using stateful firewall rules across distinct functional zones.
* **Proactive Security Operations:** Implement continuous intrusion detection (IDS/IPS), centralized log aggregation, and real-time security telemetry.
* **High-Density Containerization:** Optimize localized compute hardware to host critical network services and decoupled microservices with minimal resource overhead.
* 
* **Infrastructure Intelligence:** Integrate local, privacy-centric Large Language Models (LLMs) to dynamically query system APIs and automate operational notifications.





## Access Control \& Inter-VLAN Routing Policies



To enforce a zero-trust model without impacting administrative operations or service availability, strict stateful firewall rules are applied at the OPNsense gateway interface tiers.



### Key Traffic Flows

* **Trusted Egress to Isolated NVR:** Devices within `USER (VLAN 20)` are permitted stateful outbound access explicitly to the `reolinknvr` IP address (managed via an OPNsense Host Alias) on `IoT (VLAN 40)`. This allows local viewing applications to establish video streams while blocking the camera tier from initiating any connections back into the production network.

* **Remote Ingress Framework:** Inbound external access for off-network monitoring is currently facilitated via the NVR’s secure Unique Identifier (UID) relay mechanism. Future milestones include decommissioning this vendor-hosted relay and routing all external administrative and telemetry traffic exclusively over the **Tailscale Mesh Overlay**, maintaining complete WAN ingress isolation.

* **DNS Force-Routing:** All VLAN interfaces enforce a port-forward redirection rule that captures any outbound port 53 (DNS) requests and forces them through the local `AdGuard Home`  `Unbound` stack, preventing compromised endpoints or hardcoded smart devices from bypassing internal domain filtering policies.




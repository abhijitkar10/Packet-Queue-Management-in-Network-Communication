# High Performance Multi-Mobile Node Routing Communication Protocol

## Executive Summary

This project implements and analyzes a high-performance, reliable routing protocol for multi-mobile node networks. It focuses on enhancing packet forwarding rate, energy efficiency, end-to-end delay minimization, and network lifetime through the use of Reliable Active Nodes (RAN) and Forward Active Nodes (FAN). The protocol integrates traditional concepts with active network programming and dynamic adaptation strategies.

## Table of Contents

1. [Introduction](#introduction)
2. [Reliable Active Node Framework](#reliable-active-node-framework)
3. [Routing Protocol Design](#routing-protocol-design)
4. [ARQ Protocol Analysis](#arq-protocol-analysis)
5. [Network Simulation Results](#network-simulation-results)
6. [Performance Evaluation](#performance-evaluation)
7. [Implementation Details](#implementation-details)
8. [License](#license)

## Introduction

Modern applications like video conferencing and distance learning require reliable multicast communication. Traditional routing protocols such as OSPF suffer from limitations such as high energy consumption, low packet forwarding rates, and short network lifetimes. This project proposes an active node-based protocol to overcome these challenges.

## Reliable Active Node Framework

- **Forward Active Nodes (FAN)**: Basic forwarding, low energy, minimal reliability support.
- **Reliable Active Nodes (RAN)**: Enhanced reliability functions, active error detection, congestion control, and retransmissions.

The system follows a layered architecture and uses a Programmable Switch Approach to enable flexible reliability services in the network.

## Routing Protocol Design

- **Routing Delay Estimation**: Real-time dynamic delay calculation considering channel competition, processing, queueing, and sleep times.
- **Link Quality Assessment**: Uses Packet Reception Rate (PRR) influenced by environmental factors and hardware.
- **Next Hop Selection**: Forwarding adaptation index θ calculated based on delay, PRR, and distance to destination.
- **Adaptive Path Maintenance**: Proactive and reactive path updates, with backup paths prepared.

## ARQ Protocol Analysis

- **Go-Back-N ARQ**: Simple, but less efficient in high-error networks.
- **Selective Repeat ARQ**: More complex, but higher retransmission efficiency and network performance.

Simulations show Selective Repeat ARQ outperforms Go-Back-N under 20% error conditions.

## Network Simulation Results

- **Random Tree Networks**: Efficiency decreases with network size; hop count impacts error compounding.
- **K-Connected Graphs**: Better resilience and routing flexibility due to higher redundancy.
- **Energy Consumption**: High-traffic nodes deplete energy faster; dynamic role switching extends network lifetime.

## Performance Evaluation

- **Packet Forwarding Rate**: Improved due to active reliability work and quality link selection.
- **Energy Consumption**: Reduced by energy-aware routing and dynamic role assignment.
- **End-to-End Delay**: Minimized through accurate delay prediction and fewer retransmissions.
- **Network Lifetime**: Extended via load balancing and energy optimization.

## Implementation Details

Key components include:

- **Node Role Management**: Classify nodes dynamically as FAN or RAN based on energy, centrality, and processing power.
- **Forwarding Index Calculation**: Integrates delay, link quality, congestion, and role bonuses.
- **Next Hop Selection**: Prioritizes high-index nodes and ensures reliability for critical packets.
- **Packet Queue Management**: Uses priority queues for control, reliability, and data packets.
- **Role Transition Management**: Smooth role changes based on network conditions and energy metrics.

Example: Node role update logic

```python
def update_role(self):
    self.role = "RAN" if self.energy > 60 else "FAN"
    if self.energy > 60:
        if self.get_centrality_score() > 0.7:
            self.role = "RAN"
            self.activate_reliability_functions()
        elif self.processing_power > threshold:
            self.role = "RAN"
            self.activate_reliability_functions(limited=True)
        else:
            self.role = "FAN"
    else:
        self.role = "FAN"
        self.deactivate_reliability_functions()
```

## License

Distributed under the MIT License. See LICENSE for more information.

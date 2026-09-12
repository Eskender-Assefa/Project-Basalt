# The System Architecture

Since we have laid out the theoretical and logical architecture in the product page, we can now represent and explain the system diagramatically. Again, it is to be noted and admitted that this project is NOT production ready. It's is only meant to solve the business and technical challenges of the hackathon.

I tried drawing the system on 2 levels of difficulty. One, very minimal highliting only the important data flow, and another, focusing in detail what each part does. 

This architecture solves the core challenge of zero-trust cross-border routing failover by allowing us to scale to sub-second, telco-grade automated traffic deflection across autonomous networks while keeping infrastructure and computation costs low.

My main goal with this design is to make sure the user experience stays fast, seamless, and completely uninterrupted, even if underlying fiber links degrade or an entire peer network provider fails.

### Design 1: 

<img width="1280" height="400" alt="Passive Ingestion to EVM-2026-09-09-182859" src="https://github.com/user-attachments/assets/60a2c5ef-6c9e-4732-bfb4-bc8cfae2f62e" />

### Design 2:

<img width="1408" height="768" alt="Gemini_Generated_Image_9dyv8t9dyv8t9dyv (1)" src="https://github.com/user-attachments/assets/b3c8813b-4366-4a82-986a-688648bdf47a" />

### Zooming In: Layer-by-Layer Architectural Flow

**1. Tier 1: Continuous Ingestion Layer (data-ingestion/)**

**What it does:** Acts as the high-velocity pipeline, harvesting physical-layer metrics (laser power attenuation, bit error rates, transceiver temperatures) straight from hardware line cards using sub-second gRPC streams.

**For Engineers:** Built in Go, it scales floating-point telemetry to fixed-point integers and immediately converts them into linear secret shares. These shares are pushed onto a high-throughput Apache Kafka broker under topic streams.

**For Business Leaders:** This tier keeps operating costs negligible by handling massive telemetry ingestion pipelines concurrently without requiring expensive, dedicated hardware appliances.

**2. Tier 2: Sentinel API Gateway & SMPC Engine (sentinel-api/)**

**What it does:** Manages cross-border node communication and runs interactive, zero-knowledge calculations over the live telemetry data.

**For Engineers:** Nodes connect using mutual TLS (mTLS) with strict certificate pinning. Using an out-of-band Secure Multi-Party Computation (SMPC) loop powered by cached Beaver Triples, nodes calculate joint time-decayed health metrics and Mahalanobis anomaly scores without ever exposing cleartext fiber metrics. The resulting score feeds into a Temperature-Scaled Softmax Engine to dynamically rank alternative paths.

**Tradeoff Acknowledgment:** I chose an interactive SMPC model for cryptographic privacy and multi-node fairness, but it means I accept minor network round-trip overhead during secret-share exchange loops.

**3. Tier 3: Out-of-Band ZK-Prover (zk-prover/)**

**What it does:** Generates mathematical proof that the multi-party computations were executed honestly without altering local metrics.

**For Engineers: ** Written in Rust, this service compiles a Rank-1 Constraint System (R1CS) arithmetic circuit (mpc_in_the_head.rs). The circuit verifies that the private local metrics match public functional commitments on-chain. It stays idle until a path’s failure probability hits a 75% activation threshold, compiling a tiny Zero-Knowledge Proof string (pi).

**Tradeoff Acknowledgment:** I selected Rust for maximum memory safety and raw mathematical execution speed, but I accept higher memory usage during the short window when cryptographic proof matrices are compiled.

**4. Tier 4: Blind Arbiter Gatekeeper (blockchain/)**

**What it does:** Serves as an un-bribable public referee that authorizes path deflections.

**For Engineers:** Deployed as a stateless smart contract (BasaltFederatedVerifier.sol), it performs native bilinear pairing operations on-chain. It checks the proof string (pi) against the public cryptographic commitments published by both ISPs.

**For Business Leaders:** This slashes administrative costs and eliminates costly legal disputes over SLA breaches between peering providers by making path deflection authorization deterministic and fully verifiable.

**5. Tier 5: Executional Mitigation Agent (mitigation-agent/)**

**What it does:** The execution arm that pushes physical updates to the network switches.

**For Engineers:** Built in Python, this service remains asleep by default. It subscribes to blockchain event logs. The instant it detects an authorized block event, it wakes up, resolves the target route index against local network topology, and issues line-rate forwarding table (FIB/BGP) updates.

**For Business Leaders:** Total automation. Human operators do not need to diagnose or approve reroutes during a midnight fiber break; the system fixes the path automatically in fractions of a second.

### How We Satisfy System Reliability & Cost Efficiency

**Reliability Under Node Outages:** The decoupled design guarantees that if an external peering node goes offline or attempts to send corrupt shares, local nodes instantly catch the mismatch at the circuit layer. The system fails safe, reverting to fallback routing configurations without crashing the internal data ingestion pipeline.

**Data Flow Safety:** Information moves strictly one way through mathematical transformations—from raw physical metrics to secret shares, from secret shares to zero-knowledge proofs, and from proofs to smart contract logs. Raw telemetry never leaves the local environment.

**Cost Efficiency:** By keeping heavy cryptographic operations out-of-band and execution-triggered (Tier 3 only runs when probability thresholds are breached), Basalt operates with minimal CPU and memory footprints during baseline network operations.

## The Software Architecture

[Basalt-federated Directory including tests.txt](https://github.com/user-attachments/files/32061064/Basalt-federated.Directory.including.tests.txt)


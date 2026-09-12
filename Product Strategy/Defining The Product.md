# The Product

Now that we have synthesized the business requirements and explored the technological landscape in detail, we can lay out final solution I came up with. 

However, it is important to admit that this solution is under no circustances ready for production. This is just a protoype model that is aimed at solving the core problems presented for the hackathon. It tries to utilize technologies that are not fully mature yet (but seem necessary to solve the core problems) and search for clever methods to work around their challenges.

And so, Basalt is born...   

I named the Project as "Basalt" because one, it sounds cool, and it's short. But secondly, Basalt is a fine-grained, dark-colored igneous volcanic rock that forms when lava cools quickly at or very near the Earth's surface.  Due to its exceptional hardness, durability, and compressive strength, crushed basalt is widely used in construction and infrastructure. 

And that is precisely what we want from our product - Security, Trust, and Durability, to be the basis of infrastructure.

##  The Federated Architecture

Basalt solves the structural and business problems through a fully decoupled, multi-tier data pipeline that transitions from a passive monitoring tool to an automated execution arm during a crisis:

1. **Immediate Linear Ingestion & Sharding:** Local telemetry processors harvest physical-layer hardware performance metrics (bit error rates, optical attenuation). The data is immediately mapped to a fixed-point finite field and split into randomized mathematical shards called secret shares.

2. **Blinded Evaluation Cloud (SMPC Environment):** Competitor networks establish peer-to-peer mutual TLS (mTLS) connections. They feed these random shares through your three distinct mathematical models (Time-decayed Instability, Asymptotic Compression, and Multivariate Mahalanobis Anomaly detection) using cryptographic Beaver Multiplication Triples. The underlying calculations run entirely over blinded numbers—meaning neither network can see the other’s raw topologies or real-time metrics, yet the joint pipeline derives a unified utility score.

3. **Cryptographic Input Anchoring (Functional Commitments):** To ensure no provider cheats the math by inputting falsified, healthy parameters, both parties publish Functional Commitments (such as KZG polynomial or Pedersen commitments) directly to a private blockchain ledger. These act as immutable, encrypted seals of the actual hardware states.

4. **The Joint ZK-Prover Engine:** A specialized Rust microservice runs an MPC-in-the-head proving loop to compile a single joint Zero-Knowledge Proof (ZKP). This proof mathematically demonstrates that the outputs of the SMPC calculations were computed honestly and strictly satisfy your safety constraints (Strict Pareto Optimality, Candidate Path Integrity, and Threshold Guardrails).

5. **The Stateless Blockchain Gate:** The compact joint ZKP string is submitted via JSON-RPC to a stateless verification contract (BasaltFederatedVerifier.sol). The contract natively runs bilinear pairings to confirm the proof balances against the locked functional commitments. Once mined, it unrolls a single plain-text output: a valid path override instruction string (e.g., "PATH_09").

6. **Guarded, Inverted Agent Execution:** An isolated mitigation-agent daemon sits entirely idle, listening to the blockchain. It possesses zero decision-making power and cannot influence the ledger. The millisecond a verified block confirms the transaction, the agent awakens, interprets the path string, and flashes the local hardware Forwarding Information Base (FIB) via line-rate table adjustments.

## The Mathematical Models

**1. The Physical Telemetry Calibration Model**

Before any raw telemetry data can be evaluated, it must be standardized across varying hardware systems. Different fiber optic cables, laser transceivers, and routing switches operate under different baseline parameters, ambient temperatures, and tolerances.

This model establishes a localized baseline of what "normal" behavior looks like for every specific physical interface. It continuously measures incoming raw signals against known historical baselines, converting diverse physical measurements (like laser power attenuation, operating temperature, and bit error rates) into standardized, unitless indicators of physical stress. This ensures that a minor, safe fluctuation on a high-powered cable isn't misread as a critical failure, while subtle degrades on delicate hardware are flagged instantly.

**2. The Time-Decayed Instability Model**

Network degradation is rarely a sudden binary event; it usually manifests as a series of intermittent anomalies over time—such as brief power drops or short spikes in bit errors. A single transient glitch should not trigger a drastic rerouting, but a series of recurring glitches over a short window signals an impending collapse.

The Time-Decayed Instability model evaluates incoming physical stress indicators over a continuous time window. It applies a temporal decay weighting to historical events, meaning recent hardware stress significantly impacts the stability score, while older anomalies gradually lose influence as time passes without further issues. This prevents the system from overreacting to isolated spikes while ensuring that accumulating hardware fatigue rapidly elevates the route's risk level.

**3. The Multivariate Mahalanobis Anomaly Detection Model**

Telemetry metrics do not exist in isolation. For example, a slight drop in laser signal power might be normal if the temperature stays constant, but if laser power drops while the transceiver temperature spikes simultaneously, a hardware breakdown is highly probable. Standard threshold monitoring often misses these combined signals.

This model measures the multidimensional "distance" between current live telemetry states and healthy historical operation. Rather than looking at each metric independently, it accounts for the complex correlations between power, temperature, and bit error rates. By evaluating how all physical indicators move together, it detects subtle, correlated anomalies long before an explicit link failure occurs.

**4. The Secure Multi-Party Linear Combination Model**

Once local metrics are calculated, neighboring network providers must combine their risk scores to evaluate joint international or cross-border paths. However, neither provider is willing to share its internal metrics, as doing so would leak proprietary operational secrets.

This model allows two or more independent systems to perform mathematical addition, subtraction, and linear calculations over their combined health metrics without any party seeing the original values. It works by splitting local health metrics into masked, cryptographic shares. The nodes exchange these random-looking shares across the network, executing local calculations on the pieces. When the final result is combined, it yields the exact sum of the joint path's health, while keeping individual ISP contributions completely hidden.

**5. The Interactive Multi-Party Multiplication Model (Beaver Triples)**

While adding masked metrics together is straightforward, evaluating complex risk models requires multiplication (e.g., weighing one provider's stability against another's traffic volume). Multiplying two secret-shared numbers normally exposes the underlying secrets.

This model provides an interactive cryptographic protocol that solves non-linear multiplication over split data. By utilizing pre-computed, independent pairs of random masking factors, the two providers can engage in a lightweight, two-step data swap. This enables them to multiply their hidden metrics together and calculate non-linear risk factors without ever unmasking their private values to one another.

**6. The Temperature-Scaled Softmax Ranking Engine**

To make an automated decision on whether to deflect traffic, the system must translate raw multi-provider risk scores into concrete, actionable probabilities for every available network path.

The Softmax model converts complex, multi-variable numerical scores into a smooth probability distribution where all available path probabilities sum up to 100%. It incorporates a adjustable "temperature" parameter that controls how aggressively the system reacts to risk differences:

* **High Temperature:** Distributes traffic more evenly across multiple secondary paths, smoothing out minor operational fluctuations.

* **Low Temperature:** Sharpens the selection, forcing the system to decisively shift traffic to the single safest path the moment a primary path shows signs of degradation.

This produces a clear ranking of alternative routes, allowing the system to determine when a route's health drops below acceptable bounds.

**7. The Cryptographic Commitment Model (Pedersen / KZG)**

To prevent a malicious or compromised provider from lying during multi-party computations (e.g., fabricating healthy metrics to force traffic onto an unstable peer), the system requires strict accountability.

Before participating in joint calculations, each provider creates a binding cryptographic seal—a commitment—of its live metric state and publishes it to the shared blockchain ledger. This commitment acts like an unalterable, digital tamper-evident envelope: it locks the data in place publicly so it cannot be altered after the fact, yet it reveals zero information about the actual numbers inside to anyone inspecting the ledger.

**8. The Rank-1 Constraint System (R1CS) Zero-Knowledge Circuit**

The final layer of the architecture bridges the gap between private multi-party computation and public smart contract verification.

This model translates all the system's operational rules—such as verifying that telemetry scaling was applied correctly, confirming that secret shares match the published cryptographic commitments, and validating that a candidate path surpassed the rerouting probability threshold—into a massive system of strict algebraic constraints.

A Zero-Knowledge Prover evaluates these constraints against the private internal metrics (the "witness"). It distills the complex execution trace into a tiny, lightweight proof string. This proof mathematically guarantees to the blockchain smart contract that all calculations were performed honestly and that a route deflection is legitimately required, allowing the automated mitigation agent to safely update hardware routing tables without ever exposing cleartext telemetry.

## Unique Value Propositions (UVPs)

Basalt brings four foundational competitive advantages to enterprise and telecommunications infrastructure:

1. **Trustless Inter-Provider Federation (Co-opetition Security)**
For the first time, fierce commercial competitors can unify their automated defense infrastructures at sub-second speeds. By utilizing SMPC at the ingestion layer, ISPs can safely interconnect their automation planes without risking intellectual property leakages, commercial pricing exposures, or domestic intelligence breaches.

2. **Proactive, Zero-Latency Cryptographic Failover (The Predictive Buffer)**
Compiling multi-party cryptography and generating ZKPs takes too long to run reactively after a link completely snaps. Basalt solves this through its Predictive Buffer. Because the Temperature-Scaled Softmax model runs continuously out-of-band, the system detects a line drifting early. If a backup path crosses a designated warning threshold (e.g., a $75\%$ probability), the system pre-computes and caches the joint ZKP inside an in-memory Redis buffer before the disaster strikes. When the line fails, the failover latency is cut to microseconds, bypassing cryptographic processing delays during critical failure windows.

3. **Un-Hackable Control Plane Firewall (Inverted Execution)**
Traditional software orchestrators can be compromised to redirect global BGP routing configurations. In Project Basalt, the root of trust is shifted entirely from software to immutable mathematics. Because the mitigation agent cannot be triggered by direct API commands and only executes when a freshly mined block emerges with a contract-validated cryptographic seal, an attacker cannot force an un-anchored path deflection. If the circuit constraints fail to balance, the block never mines, and the hardware tables remain perfectly protected.

4. **Deterministic, Fully Auditable Autonomy (No AI Overhead)**
Unlike black-box machine learning models that require massive training sets, introduce unpredictable failure states, and cannot be mathematically proven, Basalt relies on rigid cybernetic control systems and deterministic equations. It is operational from day one, guarantees loop-free pathing (monotonicity), and converts directly into clean arithmetic circuit constraints—making it fully auditable for high-security national infrastructure and carrier-grade compliance.

## On Scalability

To ensure that Basalt can scale from a prototype to a production environment handling real-world internet infrastructure, we have to rethink how our software components manage data volume, cryptographic computation, and peer-to-peer networking.

Here is a breakdown of what scalability means in this specific federated, cryptographic context, followed by the core considerations we must make to achieve it.

### What Does "Scalable" Mean in This Context?

In classical software engineering, scalability usually means handling more simultaneous user requests or database reads (e.g., millions of web visitors). For Project Basalt, scalability has a highly specific, three-dimensional definition:

1. **Telemetry Velocity (The Ingestion Scale):** Carrier-grade network interfaces stream OpenConfig telemetry updates at sub-second intervals. A scalable system must ingest, process, and shard millions of these metrics per second without introducing backpressure or buffering delays.

2. **Cryptographic Density (The Compute Scale):** Running Secure Multi-Party Computation (SMPC) loops and generating Zero-Knowledge Proofs (ZKPs) requires intense polynomial mathematics and elliptic curve pairings. Scalability means ensuring that as the number of network nodes or backup paths increases, the proof generation time doesn't grow exponentially.

3. **Consensus Throughput (The Ledger Scale): **A blockchain network can become a bottleneck if it forces transactions to wait in a mempool. Scalability here means minimizing on-chain execution so that verified routing decisions clear the smart contract gate and reach the execution agent within a predictable, millisecond failover window.

### Key Considerations for a Scalable Basalt API

To handle these three scaling pressures, several critical architectural updates must be made to the API and backend modules:

**1. Decoupling High-Velocity Ingestion from Cryptographic Math**

If the API blocks inbound gRPC telemetry streams while it waits to compute an SMPC share or a vector product, the system will lag behind real-world network events.

**The Scalability Fix:** Keep the data-ingestion service entirely separate from the sentinel-api math engine. The ingestion layer should do nothing but consume raw metrics, instantly apply linear sharding, and drop those shares into a highly distributed message broker like Apache Kafka.

The sentinel-api can then pull messages asynchronously from Kafka topics using a pool of worker daemons, flattening sudden telemetry spikes without crashing the system.

**2. Optimizing SMPC via Batch Processing and Offline Triples** 

As the number of peering agreements grows, executing real-time P2P mTLS handshakes for every individual metric calculation will saturate network sockets.

**The Scalability Fix:** * Vector Batching: Instead of running the Beaver Triple multiplication protocol for a single metric line by line, batch multiple telemetry variables into a single unified matrix evaluation to reduce network round-trips.

**Pre-computed Triples:** Generate Beaver Multiplication Triples completely offline during periods of low network activity and store them in the Redis cache. When an active routing crisis occurs, the nodes simply pull these pre-generated triples out of memory, turning a heavy cryptographic operation into basic arithmetic lookups.

**3. Accelerating the Prover Layer (Hardware Acceleration & Aggregation)**

Compiling the multi-party arithmetic circuits inside the Rust zk-prover is the most CPU-heavy part of the architecture. Left unoptimized, generating a single joint proof could take seconds—far too slow for a line-rate routing failover.

**The Scalability Fix:** * GPU/FPGA Offloading: Configure the Rust prover to leverage hardware acceleration (using libraries like arkworks or cutting-edge zkVMs optimized for CUDA) to offload elliptic curve multiscalar multiplications (MSMs) to dedicated hardware.

**Proof Recursion/Aggregation:** If multiple paths are degrading simultaneously, use recursive SNARKs (like Halo2 or PLONKish circuits) to fold multiple intermediate proofs into a single, compact master proof string before submitting it to the blockchain.

**4. Reducing On-Chain Footprint (Stateless Smart Contracts)**

Executing complex array lookups or storing history directly inside a blockchain smart contract is highly inefficient and creates ledger congestion.

**The Scalability Fix:** The BasaltFederatedVerifier.sol contract must remain completely stateless. Do not store routing matrices or historical telemetry logs on-chain.

The ledger should only store a single 32-byte Merkle Root representing the current network state commitment. The transaction payload should carry the proof and the specific path updates as call data. The contract verifies the proof, updates the single state root hash, emits the event log for the agent, and discards the transient computation data immediately.

**5. Leveraging the Predictive Buffer as a Latency Shard**

The Predictive Buffer we designed is your ultimate scalability tool. It ensures that the heavy computation scales with time rather than with the crisis.

**The Scalability Fix:** By setting the pre-computation threshold guardrail carefully (e.g., starting out-of-band ZK-MPC compilation when a candidate path clears a 75% probability threshold), you distribute the CPU load over the steady-state monitoring window. When a line failure occurs, the API scales down its effort to a lightning-fast Redis cache read, isolating the active failover mechanism from any processing backlogs.

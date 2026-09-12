# The Market Alternatives

## 1. Verification & Security Protocols (The "Shields")

These are the industry-standard mechanisms used to verify that a route is legitimate.

* **RPKI (Resource Public Key Infrastructure):** As of early 2026, RPKI covers over 51% of global routes. It uses Route Origin Authorizations (ROAs) to cryptographically link an IP to its owner.  

**The Gap:** It only verifies the Origin, not the Path. It is also prone to "Invalid" states due to misconfigurations during IP leasing. 

* **BGPsec:** An extension that signs the entire path of a route.  

**The Gap:** Very low adoption due to the high CPU overhead on routers—a problem Basalt solves by moving the math off-chain.

* ** SCION (Next-Gen Architecture):** A complete redesign of the internet's routing fabric (pioneered by ETH Zürich). It is currently used by the Swiss Financial Network (SSFN) for interbank clearing.  

**The Value:** It offers path-control and millisecond-level failover.  

**The Gap:** Requires a total infrastructure replacement, making it a "hard sell" compared to Basalt’s overlay approach.

## 2. Detection & Analysis Systems (The "Eyes")

These systems identify outages and hijacks by observing the network from the outside or through telemetry.

**Cisco ThousandEyes:** The market leader in "Internet Intelligence." It provides a global view of outages and uses AI to prioritize millions of daily alerts.

**ARTEMIS: **An open-source tool for real-time BGP hijack detection. It uses a "local" view to detect anomalies in seconds but relies on human-in-the-loop for mitigation.

**Kentik:** A cloud-native platform that uses AI Agents (like "Kentik AI Advisor") to allow engineers to investigate routing spikes using natural language.  

**MANRS (Mutually Agreed Norms for Routing Security): **A global initiative where ISPs agree to implement a set of security "filters" and actions. It is a Collaborative Framework rather than a technical tool.

## 3. Collaborative Environments & Transparency

### MISP (Malware Information Sharing Platform) - Network Edition:

**What it is:** Originally for virus signatures, MISP has expanded into "Routing Threats." It allows ISPs to share "Indicators of Compromise" (IoCs) like hijacked IP prefixes.

**The Problem:** It is Human-Speed. By the time a human admin verifies a threat and uploads it to MISP, the hijacked traffic has already been diverted for minutes, if not hours.

### The BSI "Lagezentrum" (Situation Center):

**What it is:** A government-run hub where KRITIS (Critical Infrastructure) operators report outages.

**The Problem:** It is Centralized and Bureaucratic. Smaller SMEs are often left out of the loop because they don't meet the "Criticality Threshold," leaving them blind during a regional crisis.

### MANRS (Mutually Agreed Norms for Routing Security) Observatory:

**What it is:** A collaborative "Social Contract" where ISPs provide telemetry to prove they aren't the ones causing hijacks.

**The Problem:** It is Reputational, not Enforcement-based. It tells you who is a "bad actor" after the fact, but it cannot physically stop a bad route from spreading.

## ... More tools used for collaboration and transparency

### 1. PeeringDB: The "Yellow Pages" of the Internet

In 2026, PeeringDB remains the first stop for any network engineer. It is a user-maintained database where ISPs, Data Centers, and IXPs list their "Handshake Rules."

**The Transparency Value:** It tells you where a network is located, who to call if their routers break, and what their "Peering Policy" is (e.g., "Open" vs. "Restrictive").

**The 2026 Shift:** PeeringDB has recently moved toward Location Data Normalization (March 2026) to help automate interconnection decisions.

**The Failure Point:** It is a Static Database. It tells you what a network intends to do, but it cannot tell you what a network is actually doing right now. If a hacker hijacks a route, PeeringDB doesn't turn red—it just sits there.

### 2. BGPStream: The "CCTV" of the Internet

BGPStream is the industry’s primary open-source framework for analyzing routing data in real-time. It acts as the "Crime Scene Camera" for the internet.

**The Transparency Value:** It aggregates data from global sensors (like RIPE RIS and RouteViews) to detect Route Leaks and Hijacks.

**The 2026 Reality:** High-profile incidents, like the Cloudflare Route Leak in January 2026, are analyzed using BGPStream data to prove exactly when and where a "valley-free" routing rule was violated.

**The Failure Point:** It is Post-Facto & Unverified. BGPStream tells you a robbery is happening, but it cannot lock the door. Furthermore, it relies on "observing" the internet from the outside, which means it can be tricked by sophisticated attackers who "spoof" the telemetry.

### 3. PEC (Privacy-Enhancing Computation): The "Swiss Vault"

As of April 2026, the PEC market has grown to $7.28 Billion. It is a family of technologies (including ZKPs, SMPC, and Homomorphic Encryption) that allows parties to work together without actually seeing each other's data.

**The Transparency Value:** PEC allows the ALL#HANDS partners to calculate a "National Risk Score" without any single ISP having to reveal their proprietary customer list or internal topology.

The Tools of the Trade:

**SMPC (Secure Multi-Party Computation):** Multiple ISPs jointly compute an outage map; no one ISP sees the whole map, but they all see the final "Safe" result.

**ZKP (Zero-Knowledge Proofs):** An ISP proves they have a valid path to a bank without showing the actual router IPs along that path.

**The Failure Point:** High Complexity & Latency. Most PEC tools in 2026 are still too slow for "Wire-Speed" networking. They are used for planning and auditing, but not for routing packets in milliseconds.

# The Problem Statement

I generally like to follow a Design Thinking approach to fully capture both the bird's eye view AND the small details. I had taken an intensive workshop on Design Thinking a few months back, and I have to say, it is perhaps one of the best business concepts I ever learnt.

## What is the Problem?

The hackathon poster gives us a set of 3 starting points:

* The internet becomes overloaded & sometimes fails completely. 

* There appears to be a gap in detecting/analyzing network disruptions & visualizing them in a clear/understandable way for network operators.

* Some gaps must exist in creating transparency, explaining outages & strengthening digital resilience.

I go layer by layer, and deeper into the core matter.

### I ask the 1st wave of questions.

**1. Why the Internet Still Overloads and Fails**

Despite advancements in fiber and 5G, the "bottleneck" effect remains a physical and economic reality.

* **The Data-to-Infrastructure Gap:** Global data traffic is growing at an exponential rate (driven by AI model training, high-definition streaming, and IoT), while physical infrastructure deployment is linear. Laying cables and building data centers takes years; launching a new high-bandwidth app takes seconds.

* **Legacy Protocols:** Much of the internet still relies on BGP (Border Gateway Protocol), designed in the 1980s. It wasn't built for modern security or massive traffic rerouting, leading to "route leaks" that can knock out entire regions.

* **The "Middle-Mile" Issue in Germany:** While Germany has strong international backbones (like DE-CIX in Frankfurt), the "last mile" and "middle mile" in rural or industrial areas often still rely on aging copper lines or over-provisioned local nodes that cannot handle peak-time surges.

**2. The Gap in Detection and Visualization**

The note mentions a failure to visualize disruptions for operators. This is a "data noise" problem rather than a "lack of data" problem.

* **Fragmented Ownership:** No single entity "owns" the internet. A signal might pass through five different providers' networks. When a disruption occurs, operators often only see that their traffic has stopped, but they cannot "see" into the third-party network where the actual failure occurred.

* **Visual Overload:** Modern networks generate millions of log lines per second. Creating a "clear and understandable" dashboard requires sophisticated AI to filter out noise, which many legacy Network Operation Centers (NOCs) haven't fully integrated yet.

* **Lack of Standardization:** Different hardware vendors (Cisco, Huawei, Nokia) use different telemetry formats. Normalizing this data in real-time to create a unified "map" is a massive technical hurdle.

**3. Transparency and Digital Resilience Gaps**

Resilience isn't just about fixing things when they break; it’s about knowing they might break before they do.

* **Commercial Secrecy:** Transparency is often at odds with competition. Providers are hesitant to share real-time health data of their networks because it might expose vulnerabilities to hackers or reveal weaknesses to competitors.

* **The Skills Gap in Germany:** The German IT sector faces a significant shortage of specialized network engineers and cybersecurity experts. Without the human capital to implement complex resilience frameworks, companies stick to "reactive" rather than "proactive" maintenance.

* **Bureaucracy and Regulation:** In Germany, strict data protection (GDPR) and infrastructure regulations can sometimes slow down the implementation of deep-packet inspection or shared monitoring tools that would otherwise improve transparency.

### I ask the 2nd wave of questions

* Why does most of the internet still rely on legacy protocols like BGP? What specific flaws does BGP have that leads to route leaks?

* Why does Germany still use aging copper lines & over-provisioned local nodes for last-mile network operations?

* Why haven't legacy network operation centers (NOCs) still fully integrated the complex AI to present the data on a dashboard in an understandable way?

* Why is it such a big technical hurdle to normalize the data & create a map of the diff telemetry formats? Why hasn't the industry moved towards one telemetry format?

* What about data regulations slow down the implementation of deep-packet inspection & sharing monitoring tools?

### ...the possible answers

**1. The Persistence of Legacy Protocols (BGP)**

* **Why it persists:** The Border Gateway Protocol (BGP) is the "glue" of the internet. It survives because replacing it requires global consensus among thousands of independent Autonomous Systems (AS). There is no "Internet CEO" to force an upgrade.

* **BGP Flaws & Route Leaks:** Lack of Native Validation: BGP was built on implicit trust. It doesn't automatically verify if a network actually owns the IP addresses it claims to have.

* **The "Shortest Path" Logic:** BGP prefers the shortest hop count. If a small network accidentally announces a "shorter" (but false) path to Google, traffic globally will divert to that small network, causing an overload and a "leak."

* **Human Error:** Most leaks are simple typos in configuration files that the protocol is too "dumb" to catch before broadcasting globally.

**2. Germany's Aging Infrastructure (Copper & Last-Mile)**

* **The "Vectoring" Decision:** Historically, Germany’s dominant providers chose to "squeeze" more speed out of existing copper wires using Vectoring technology rather than digging up streets for fiber (FTTH).

* **Economic Sunk Cost:** It was significantly cheaper and faster to hit government broadband targets by upgrading copper than by installing new fiber.

* **Regulatory Hurdles:** Digging in Germany involves complex municipal permits and high labor costs. This created a "digital divide" where urban nodes are over-provisioned (too many users on one local node), leading to evening slowdowns.

**3. AI Integration in NOCs (The Dashboard Gap)**
Why NOCs are lagging:

* **Data Silos:** Network data isn't just one stream; it’s SNMP, streaming telemetry, Syslogs, and flow data. Traditional AI struggles with these "unstructured" and non-standardized formats.

* **The "Black Box" Problem:** Network operators are risk-averse. If an AI suggests rerouting traffic but can't explain why, humans are hesitant to trust it. They prefer a messy, manual dashboard they understand over a "clean" AI dashboard they don't.

* **Real-time Processing Power:** Analyzing petabytes of telemetry in milliseconds to provide "intelligent" visualization requires massive compute power that many local NOCs simply don't have on-site.

**4. The Telemetry Normalization Hurdle**

Why no "One Format"?

* **Vendor Lock-in:** Hardware giants (Cisco, Juniper, Huawei) have a financial incentive to keep their telemetry formats proprietary. It makes it harder for a customer to switch to a competitor’s equipment.

* **Standardization Lag:** Groups like the IETF work on standards (like gNMI), but by the time a standard is ratified, new hardware features have already been released with new, non-standard telemetry needs.

* **The Translation Tax:** Normalizing data requires "middleware" that adds latency. In a world where milliseconds matter, many operators prefer raw, messy data over "clean" delayed data.

**5. Data Regulations vs. Deep-Packet Inspection (DPI)**

In Germany and the EU (GDPR), the "privacy of telecommunications" is a fundamental right.

* **Deep-Packet Inspection (DPI):** This involves looking at the content (payload) of a packet, not just the header. In Germany, this is often legally restricted unless there is a specific security threat, as it can be seen as "mass surveillance."

* **The Paradox of Sharing:** Sharing monitoring tools often means sharing metadata that could identify specific users or businesses. Under GDPR, this "anonymization" process is technically difficult to do in real-time without stripping away the data that makes the monitoring useful in the first place.

* **Compliance Liability:** For a network operator, the risk of a GDPR fine is often perceived as greater than the risk of a minor network outage, leading to a "play it safe" approach that limits transparency.

### ...Then a 3rd wave of questions.

* Why does BGP lack native validation? How does this directly contribute to the route leaks?

* What sort of human errors contribute directly to route leaks? What is the extent at which these human errors occur?

* Until when or upto which extent does vectoring technology continue to be a 'solution' to the infrastructure problem? What then?

* Why does traditional AI struggle with the different types of network data? How does the unstructuredness & non-standardizedness impact the AI adoption?

* How long does it take to ratify a standardization of telemetry data? How fast do the hardware features change, why do they change?

### ...Possible answers

1. BGP's Lack of Native Validation & Route Leaks

* **The "Why" of the Lack of Validation:** BGP was finalized in 1989, an era when the internet consisted of a small number of trusted academic and government institutions. Security was not a design requirement; reachability was.

* **Trust by Default:** BGP messages are just plain text. When an Autonomous System (AS) says, "I have the best path to Amazon," other routers believe it without checking a "ID card."

* **The Complexity of Change:** To add native validation, every router on Earth would need a software (and often hardware) upgrade simultaneously. Instead, we use "patches" like RPKI (Resource Public Key Infrastructure), but adoption is voluntary and currently sits at only about 40-50% globally.

How it leads to leaks:

A route leak happens when a "No-Export" or "Internal" route is accidentally "leaked" to the public internet. Because there is no native validation, the rest of the world accepts this "leak" as a valid new path, often pulling massive amounts of traffic into a network that can't handle it (the "Black Hole" effect).

**2. The Human Factor: Errors and Frequency**

Human error is cited as the cause for over 60-80% of all BGP incidents.

Types of Errors:

* **The "Fat Finger":** A simple typo in a Prefix List (e.g., typing 10.0.0.0/8 instead of /18) can accidentally announce the entire internet's traffic to a single small router.

* **Filter Misconfigurations:** Forgetting to apply a "Route Map" that tells a router not to share its provider's routes with another provider.

* **Extent:** According to groups like MANRS (Mutually Agreed Norms for Routing Security), there are dozens of BGP incidents every single day. Most are small, but once or twice a year, a "Global Leak" occurs (like the 2019 Cloudflare/Allegheny leak) that disrupts millions of users.

**3. Germany’s "Vectoring" Trap: Copper’s Expiration Date**

Why Vectoring? In the mid-2010s, Germany leaned heavily into Vectoring (noise-canceling for copper wires) to hit speed targets of 100-250 Mbps quickly. It was a "band-aid" that postponed the expensive task of digging up streets for fiber.

Until when? Vectoring has hit its physical limit. You cannot "vector" your way to 1,000 Mbps (Gigabit) speeds over long copper distances.

**The Transition:** Germany is currently in a "Fiber Sprint." The goal is for 25 million households to have FTTH (Fiber to the Home) by 2030.

What then? Once the copper is turned off, the "over-provisioned local nodes" (the grey boxes on street corners) will be replaced by passive optical splitters, which don't require power and don't "overload" like the old electronic nodes.

**4. Why Traditional AI Struggles with Network Data**

AI is only as good as its training data, and network data is a mess.

* **Unstructuredness:** A network generates "Flow" data (who is talking to whom), "Logs" (text sentences about errors), and "SNMP" (simple number counters). Combining these is like trying to write a book using a dictionary, a spreadsheet, and a series of post-it notes.

* **Non-Standardization:** If Cisco calls a "link failure" Type-1 and Juniper calls it Error_404, an AI can't easily correlate them.

* **Impact on Adoption:** Because AI models currently require massive "cleaning" of this data (Data Engineering), the Time-to-Value is too long. Operators find it faster to just look at a raw log than to build a "cleaning pipeline" for an AI.

**5. The Standardization Lag vs. Hardware Speed**

* **Ratification Time:** To get a new telemetry standard (like a new version of IPFIX or gNMI) through the IETF (Internet Engineering Task Force), it typically takes 3 to 5 years.

*** Hardware Speed:** Chip manufacturers (Broadcom, NVIDIA/Mellanox) release new silicon every 18 to 24 months.

* **The Conflict:** By the time a "standard" is agreed upon for how to report, say, "Quantum-resistant encryption latency," the hardware has already moved on to a new feature that the standard doesn't cover.

Why change? Hardware changes to meet the demand for speed (throughput). Telemetry standards change to meet the demand for visibility. Speed always wins the budget race, so visibility is always playing catch-up.

### ...After this research, it was started to become clearer what a good solution might look like.

* The Self-Healing BGP Filter (Security & Automation)

* Universal Telemetry Translator (Data Normalization)

* Predictive Congestion Mapping for Germany (Resilience)

### ... and some technologies that seemed interesting to solve the challenges.

* **Agentic AI (LLM Agents):** Instead of a static dashboard, use an AI Agent that can "reason" through logs. Example: "Hey Agent, why is the Frankfurt node at 90% capacity?" The agent then checks BGP routes, latency, and power logs to give a plain-English answer.

* **Edge Observability:** Instead of sending all data to a central NOC (causing lag), perform AI Analysis at the Edge. Process the telemetry directly on the router or a local server to catch "Micro-bursts" of congestion that a central system would miss.

* **Zero-Knowledge Proofs (ZKP):** Use ZKPs to solve the "Transparency vs. Privacy" problem. Providers can prove their network is healthy to partners without revealing their internal topology or sensitive customer data, satisfying German GDPR requirements.

* **Blockchain:** It prevents unilateral revocation. An ISP can post a "Proof of Health" or "Proof of Outage" to a shared ledger. Other ISPs can verify the proof is mathematically true without seeing the underlying sensitive data (like which specific customers are affected or the exact hardware topology). It creates a "Black Box" for the internet. If a human makes a "Fat Finger" error and then tries to hide it by deleting local logs, the blockchain record remains. This is crucial for the "Digital Resilience" Germany is pushing for in 2026 under the new BNetzA security overhaul.

### ... Question:

* Why hasn’t this solution so far been implemented?

**1. The "1000x" Overhead ProblemCurrently, generating a Zero-Knowledge Proof (ZKP) is computationally "expensive."** 

* **The Math Gap:** According to recent research from Nokia Bell Labs, the overhead for ZKP techniques needs to drop by 1,000x before they are practical for high-speed routing.  

* **The Latency Trap:** A core internet router handles millions of packets per second. If it stops to generate a complex mathematical proof for every announcement, the "lag" would make the internet unusable. We are currently waiting for hardware acceleration (specialized ZKP chips) to make this happen in real-time. 

**2. The "Incentive" Catch-22 (Who pays?)**
The internet is a collection of private businesses (ISPs).

* ** Cost of Entry:** Implementing a blockchain-based BGP system requires every major ISP to upgrade their hardware and software simultaneously.

* **The First Mover Disadvantage:** If Deutsche Telekom upgrades but Vodafone doesn't, Telekom pays the "tax" of higher compute costs and complexity while Vodafone gets a "free ride" on the increased security. Without a global mandate, no one wants to be the first to pay the bill.

**3. The Standardization War**

As of 2026, the National Institute of Standards and Technology (NIST) is still in the process of standardizing ZKP protocols.

* ** Vendor Lock-in:** Cisco, Juniper, and Huawei all want their version of the truth to be the standard. Until there is a "Universal Language" (like what we proposed for Project Hack), these systems can't talk to each other. A blockchain is useless if every node is running a different, incompatible version of the software.

**4. Regulatory Fear & "Opt-In" Privacy**
In Germany and the EU, regulators are cautious.

* **The "Black Box" Fear:** While ZKPs protect privacy, they also make it harder for law enforcement to track malicious actors. There is a "regulatory friction" where governments want transparency for themselves but not necessarily for the public.

* **Complexity:** Most network admins are trained in traditional protocols (BGP, OSPF). Moving to a "Web3-style" decentralized network requires a massive retraining of the global workforce.

### ... more questions

* Why is current zkp price so high? And why does Nokia want it to be at least less than 1000x?

### ... Possible answers

**1. Why is the ZKP "Price" so high?**

In the world of networking, "price" isn't just money—it's CPU cycles, latency, and power. Currently, generating a proof is roughly 10,000 to 1,000,000 times more expensive than simply performing the underlying computation.

* **The Math Explosion:** To create a Zero-Knowledge Proof, a simple network operation (like "Route this packet to Munich") must be converted into a massive system of algebraic equations (often called a "circuit"). A single routing decision can turn into millions of these equations.  

* **The Prover's Burden:** Solving these equations requires heavy cryptographic operations like Multi-Scalar Multiplication (MSM) and Number Theoretic Transforms (NTT). These tasks are "brute-force" math that can max out even high-end GPUs.  

* **Memory Bottlenecks:** Generating proofs requires huge amounts of RAM to store the intermediate "witness" data. For a high-speed router handling terabits per second, the memory requirements for ZKPs would currently physically exceed what can fit inside the box.

* **The Latency Killer:** In 2026, network operators aim for "micro-latency." Generating a complex ZKP can take anywhere from a few seconds to several minutes. In a network where every millisecond counts, a 5-second "wait for proof" is an eternity.

**2. Why does Nokia (and the industry) want a 1000x reduction?**
The 1000x goal is the "Magic Threshold" where ZKPs move from being a specialized niche to being native to the hardware.

**A. The Speed of Light vs. The Speed of Math**
Internet routers operate at Line Rate (processing packets as fast as the electricity/light moves through the wire).

**The Problem:** Current ZKP generation is "Off-Line"—you do the math later.

**The Goal:** By reducing the overhead by 1000x, the math becomes fast enough to happen "In-Line." This would allow a router to sign a "Proof of Health" for a packet while the packet is moving through the port, without slowing it down.

**B. Energy Sustainability**

Nokia’s recent 2026 reports emphasize "Sustainable AI-Nativeness."If ZKPs remain 1,000,000x more expensive, securing the internet with them would consume more electricity than the rest of the global network combined.A 1000x reduction brings the power consumption of "Proven Security" down to a level that is economically and environmentally viable for mass deployment.

**C. Consumer Device Integration**

For the current ZK proposition to work, even small local nodes or "edge" devices (like the ones in German neighborhoods) need to participate.Currently, you need a $20,000 server to be a "Prover."  A 1000x reduction allows the Prover to run on a standard smartphone chip or a low-power IoT sensor. This "democratizes" the security, so even a small local ISP in rural Germany can prove its network is secure without buying a supercomputer.



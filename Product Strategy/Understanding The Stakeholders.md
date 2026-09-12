# The Stakeholders

Building a great product involves understanding the stakeholders involved and their motivation on a big part. This gives us a polished understanding of the business requirements and build something that somewhat satisfies each party's core problem.

## Who are the organizers of the hackathon and what do they want?

The program is hosted by ALL#HANDS, a government initiative to strengthen Germany’s overall digital resilience and SMEs who are struggling with network issues, endorsed by the Federal Ministry of Research and Innovation (BMFTR). The program was sponsored by Leitwert GmbH, an Ingolstadt based internationally recognized internet network intelligence firm. The event was to be attended by several ISPs like Deutsche Telekom. They would have been among the judges.

I orgnaized each participating/concerned party and their POV statements as follows:

### 1. ALL#HANDS & BMFTR:

* They want ISPs to share internal telemetry data to create a national situation picture, but they are held back by economic and legal hurdles.

* They want to map ISPs interdependencies on hardware/software usage, but ISPs are refusing to share sensitive data. There is no central physical infrastructure registry.

* It is becoming increasingly hard to cope with network outages as there is no normalization of data and every organization looks at different data during outages.

* They are observing that SMEs (backbone of German economy) are being hurt during network outages and cannot deal with it themselves. So they want to create an easy-to-understand citizen Information system.

**POV statement:** National security strategists and regulatory bodies **need** a normalized, real-time registry of hardware interdependencies and ISP telemetry **because** they are currently attempting to manage a national security interest with "broken binoculars." The **insight** here is that a unified "national situation picture" is impossible to maintain when every guardian is looking at a different, fragmented map; without standardized data and forced transparency of infrastructure, the speed of a cyber crisis will always outpace the government's ability to coordinate a response.

### 2. SMEs:

* Revenue bleed of 5000 EUR – 20,000 EUR per hour of network outage. Lost sales, employees paid for free.

* A trust decay with customers and loss of reputation

* The Liability of managing directors for cybersecurity failures and fines of up to 2% of global turnover.

* Reporting nightmare. They are required to report a disruption in 24 hours. They don’t have a system to detect let alone to report.

* They have a huge, trained talent vacuum.

* They use legacy hardware/software that isn’t designed for the modern/chaotic environment.

* Visibility gap. They have 0 knowledge why their connection is slow or where their data is going.

* It is still based on reactive measures.

* They are too small to demand better security from massive ISPs. They are price takers in a market that prioritizes speed and volume over verifiable security.

**POV statement:** Managing directors of German small-to-medium enterprises **need** an automated, easy-to-understand "early warning" system that provides visibility into connection failures without requiring specialized in-house talent. The **insight** is that for these businesses, a network outage is no longer just a technical nuisance but a legal and financial existential threat, where the combined pressure of revenue bleed
and massive NIS2 liability fines makes the cost of "not knowing" far higher than the cost of the security service itself.

### 3. Leitwert:

* They are left in blind spots to give a ‘German situational picture’ as every ISP is secretive about data over competition and privacy laws. They cant find a neutral ground to aggregate data without owning or seeing it.

* They can detect hijacks and leaks but mitigation falls on human to human interaction. Network operators are terrified of automation bugs.

* Inability to simulate a crisis with little real-time ground truth of how the network behaves under stress. Most data they have is from good days. On bad days, sensors fail or data becomes too chaotic to model. This is a lack of high fidelity telemetry. They have maps of the internet but not the live GPS traffic for every single route.

**POV statement:** Network analysts and crisis simulation architects **need** access to high-fidelity "bad day" telemetry and a neutral ground for data aggregation to move mitigation beyond slow human-to-human interaction. Their **insight** is that strategic defense is currently dangerously built on "fair-weather" data; without real-time "GPS-style" traffic visibility for every route, the network remains a black box where sensors fail exactly when they are needed most, leaving the country unable to simulate or survive a true digital stress event.

### 4. ISPs:

* Regulatory pressure from the NIS2 Directive and the German BSIG 2.0, which has scared managing directors and increased liability issues.

* Looking for basic foundational remedies to their problems that make economic sense.

* Government is forcing them to work together to avoid global attacks. Working together requires exchanging data.

* Price for internet services has leveled. They are looking for new excuses/innovations to increase price with low churn.

**POV statement:** Executive leadership at Internet Service Providers **need** foundational, economically viable remedies to satisfy NIS2/BSIG 2.0 mandates while discovering new innovations that justify price increases in a leveled market. The **insight** is that ISPs currently view government-mandated data sharing as a threat to their competitive secrets and profit margins; they will only transition from being "secretive gatekeepers" to "collaborative partners" if the burden of regulation can be rebranded as a premium, low-churn value add for their customers.

### The Digital Twin POV (The Simulation Gap)

Emergency Planning Authorities **need** a high - fidelity digital twin of the German internet **because** we cannot safely test 'What If' scenarios —like a massive power failure or a core - router software bug —on the live, production network without risking the very stability we aim to protect.


### Since the event was funded by _Leitwert GmbH_, a little bit more about them...

To understand Leitwert, we have to understand **HEAP** (Hijacking Event Analysis Program). Developed primarily by their founders (like Dr. Johann Schlamp), HEAP isn't just a tool; it is the scientific foundation that Leitwert was built upon.

**1. What does HEAP do?**

HEAP is an automated system designed to solve the "False Alarm" crisis in BGP security.

* **The Problem:** Most BGP monitors flag any weird route change as a "Hijack." In reality, 90% of these are legitimate operational changes (like an ISP moving traffic for maintenance).

* **The Goal:** HEAP’s job is to "disprove" malicious intent. It filters through the noise to find the 1% of truly dangerous, deliberate attacks.

**2. How does it function? (The "Triple - Filter" Logic)**

HEAP doesn't just look at one data point; it uses a multi - layered reasoning engine:

* **Business Logic Filter:** It checks Internet Routing Registries (IRRs) to see if the two parties involved in a route change actually have a business relationship (e.g., a customer/provider link). If they do, it’s likely not a hijack.

* **Topology Reasoning:** It uses a complex algorithm to see if the new "shorter" path is even physically/topologically possible in a legitimate setup.

* **The "Key" Witness (SSL/TLS):** This is the genius part. HEAP scans the internet to identify SSL/TLS certificates. If a route changes, HEAP checks if the public key of the website at the end of the path stayed the same. If the key changed, someone is likely impersonating the site (a Man - in- the- Middle attack).

**3. Why is it so great and different?**

* **It’s Evidence - Based:** Before HEAP, BGP security was mostly "guessing." HEAP introduced a formal, mathematical model of Internet routing.

* **It Focuses on the "Elaborate" Attacker:** Most tools catch "stupid" mistakes. HEAP is designed to catch AS - Path Manipulation, where a sophisticated attacker makes their fake route look perfectly normal to standard filters.

* **Non- Invasive:** It doesn't require ISPs to install new hardware. It sits on the side and
"listens" to the global heartbeat of the internet.

**4. What is Important to Leitwert?**

* **Scientific Grounding:** Leitwert was founded by researchers (notably Dr. Johann Schlamp) who literally wrote the book (and award - winning papers) on BGP
hijacking detection . They value mathematical proofs over marketing buzzwords.

* **Real - Time Actionability:** Their flagship "Anomaly Monitor" and "Hijacking Event Analysis Program (HEAP)" are designed to assess the legitimacy of routing alarms in real - time. Any lag in your solution is a red flag for them.

* **Privacy - Preserving Collaboration:** As a partner in the ALL#HANDS project, they are tasked with building a "low - risk" way to share data. They are obsessed with how to aggregate sensitive ISP logs without violating GDPR or exposing proprietary network topologies.

* **Infrastructure Resilience:** They aren't just looking at software; they are looking at how the "bones" of the internet (peering points, transit links, and IXPs) stay stable during power outages or software errors.

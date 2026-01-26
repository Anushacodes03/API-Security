# API Security Notes

## What are APIs?

**API = Application Programming Interface**
- Often called "websites for machines"
- Present in almost everything we do online

### Common Examples
- **Google to Lyft/Uber**: Communication for ride booking
- **Venmo to Wells Fargo**: Money transfers between accounts
- **Kayak to Airlines**: Fetching airfare information across multiple carriers

APIs power the modern internet and enable integrations across organizations, applications, and mobile apps.

---

## The Perfect API Storm: Key Statistics

### 83% - Internet Traffic
- Percentage of internet traffic that is API-powered
- Study by Akamai demonstrates API pervasiveness
- APIs power virtually every website and mobile app

### #1 - Attack Vector Ranking
- Gartner predicted API attacks would become the top attack vector
- This prediction has proven accurate

### 4% - Security Testing Gap
- Survey by RapidAPI (now Nokia) of millions of users
- **96%** perform positive testing (functionality, bugs, performance)
- Only **4%** conduct security testing on APIs
- This creates a perfect storm for breaches

---

## What Makes APIs Attractive Targets?

### Data Access
APIs connect to:
- Transaction engines
- Personal information
- Corporate intellectual property
- Credit card information

### Attacker Motivations
- Stealing credit card data
- Stealing personal information
- Performing fraud
- Scraping data

---

## Why APIs Are Vulnerable

### The Glue of the Internet
- APIs sit between application functionality and backend systems
- Every action (login, deposit check, transfer money) is an API call
- Connect the outside world to internal applications, databases, and transaction engines
- Flaws in configuration or logic become vulnerabilities

### APIs Are NOT Hidden
**Example: United Airlines Website**
- Right-click → Inspect → Network tab
- Easily reveals API calls like "Fetch Flights"
- Can view entire payload and request construction
- Attackers use this same simple method

---

## How API Attacks Occur

### Attack Process
1. Attacker creates account/installs mobile app
2. Uses every feature and function
3. Monitors traffic for API calls
4. **Bypasses UI to hit APIs directly**

### Why Bypassing UI Works
- **UI Layer**: Controlled, locked down
  - Only shows intended data
  - Only allows intended actions
- **API Layer**: Uncontrolled
  - Just a command line
  - Can write any request
  - Backend must validate legitimacy

### Common Vulnerabilities Found
- **Over-permissioned APIs**: Access to more data/functionality than exposed in UI
- **Logic flaws**: Not exploitable in UI but exploitable at API layer

---

## Attack Complexity Comparison

### Classic Cyber Attack "Kill Chain"
Multi-step, complex process:
1. Reconnaissance
2. Infiltration
3. Weaponization
4. Lateral movement
5. Privilege escalation
6. Exfiltration/breach

Requires high sophistication most attackers lack.

### API Attack
Simple two-step process:
1. Probe for vulnerability
2. **Go straight to breach**

Much simpler attack pattern makes APIs appealing targets.

---

## Regulatory Landscape

### Real-World Examples

**T-Mobile Breach**
- 37 million subscriber records exposed
- Unauthorized API access
- Required SEC 8-K filing

**Verizon (TracFone)**
- $16 million FCC fine
- Subscriber data leaked through APIs
- Mandated API security best practices including:
  - Continuous static and dynamic security testing
  - Automated vulnerability testing
  - Prioritization of API testing

### Key Regulations

**PCI DSS 4.0** (Payment Card Industry)
- Mandatory since 2024
- Requirements include:
  - Business logic abuse detection
  - Abusive API monitoring
  - Developer training on API risks

**GDPR** (Privacy)
- Applies when APIs touch personally identifiable information (PII)

**HIPAA** (Healthcare)
- Applies when APIs handle Protected Health Information (PHI)

**SEC Regulations**
- Four-day breach notification requirement
- Publicly traded companies must report security programs
- Must include API risks

**UN Cybersecurity** (Automotive)
- Requirements for automotive manufacturers and suppliers
- Connected cars powered by APIs (unlock doors, air conditioning, etc.)

**FedRAMP** (US Government)
- Monthly web application security vulnerability testing
- Includes APIs for cloud services to US government

---

## Three Core Regulatory Requirements

### 1. Security
Ensure secure operations of infrastructure and applications where APIs are used.

### 2. Privacy
Protect individual data (GDPR, CCPA, PIPEDA, etc.). APIs accessing regulated information must be part of threat modeling and risk profiles.

### 3. Data Accessibility
**Competing requirement**: Organizations must make data portable and accessible through APIs (HIPAA, banking regulations) while ensuring secure transfer.

---

## Key Takeaways

- APIs are fundamental to modern internet operations
- Massive security testing gap (4% vs 96%)
- APIs are easily discoverable, not hidden
- Simpler attack patterns than traditional cyber attacks
- Regulators are increasingly focused on API security
- Organizations must balance security, privacy, and accessibility
- Proactive, continuous testing is essential

---

## Next Steps

The course will cover:
- OWASP Top 10 API vulnerabilities
- Real-world breach examples
- Detailed attack methodologies
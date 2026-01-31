# OWASP API Security Top 10 - Course Notes

## Introduction to OWASP

### What is OWASP?
- **Full Name**: Open Worldwide Application Security Project
- **Type**: Non-profit organization
- **Purpose**: Produces leading guidance for application security
- **Best Known For**: OWASP Top 10 for Web Applications

### OWASP API Security Top 10

#### History and Evolution
- **2019**: OWASP recognized that APIs have unique threats and risks distinct from web applications
  - Created the first OWASP API Security Top 10
  - Acknowledged APIs deserve their own dedicated security framework

- **2023**: Updated edition released
  - Some items added
  - Some items changed
  - Some items deleted from the 2019 version
  - This course covers the **2023 edition**

## Course Structure

### Approach
Each item in the Top 10 will be broken down into separate submodules covering:
1. **Description** - What the vulnerability/risk is
2. **Real-world Example** - Demonstration of the risk vector
3. **Best Practices** - Guidance and recommendations for prevention

## Real-World API Attacks

### Current Threat Landscape
- **Volume**: Enormous number of successful API attacks, breaches, and exploits occurring
- **Publicity**: Many attacks are becoming publicized incidents
- **Variety**: Multiple threat vectors being exploited

### Common Threat Vectors Observed

The following threat vectors are being seen in real-world API attacks:

1. **Unauthorized Trading**
2. **Account Data Harvesting**
3. **Data Exposure**
4. **Takeovers**
5. **Tampering**
6. **Reputation Risk**
7. **Ransom**
8. **Third Party Exposure**

### Key Insight: Why APIs Are Vulnerable

#### The Defense Gap
Despite organizations employing comprehensive security measures, API attacks continue to succeed:

**Common Security Measures in Place:**
- Web Application Firewalls (WAF)
- Source code scanning
- Dynamic testing
- Penetration testing
- Industry best practices

**The Problem:**
Something about API attacks is getting through these traditional defenses. This gap between traditional security controls and API-specific threats is what makes API security uniquely challenging.

## Course Objectives

This course will explore:
- Why traditional security measures aren't fully effective against API attacks
- Specific vulnerabilities outlined in the OWASP API Security Top 10 (2023)
- How to identify and mitigate each type of API security risk
- Real-world examples mapped to each OWASP category
- Best practices for securing APIs

---

## Next Steps

The course will begin with **OWASP API Security Risk #1** and progress through each item in the Top 10, providing detailed analysis and practical guidance.

---

## Additional Resources

- OWASP Official Website: https://owasp.org
- OWASP API Security Project: https://owasp.org/www-project-api-security/
- OWASP API Security Top 10 2023: https://owasp.org/API-Security/editions/2023/en/0x00-header/

---

# OWASP API Security Top 10 - Detailed Breakdown

## #1: Broken Object Level Authorization (BOLA)

### Overview
- **Also Known As**: BOLA
- **Ranking**: #1 in both 2019 and 2023 editions
- **Severity**: One of the most dangerous and difficult to detect threats

### What is BOLA?

**Definition**: Authorization flaws that allow unauthorized access to objects or data belonging to other users.

**Classic Examples:**
- Can User A access User B's data?
- Can a user perform an action on an unauthorized object?

**Key Characteristics:**
- Authorization flaws (not authentication)
- Difficult to detect at runtime
- Can cause significant data loss
- Can enable fraudulent transactions

---

### Real-World Example #1: Coinbase Unauthorized Trading

#### The Discovery
A security researcher tested the Coinbase platform by:
1. Creating an account
2. Depositing money
3. Using platform features while monitoring API traffic
4. Analyzing trade API requests

#### The Vulnerability

**Normal Trade Request Structure:**
```
Quantity: [amount]
Price: [price]
Product ID: [asset type]
Account: [user account]
Side: SELL
```

**The Test:**
- Researcher owned Ethereum on the European market
- Made a valid sell request for their own Ethereum
- Then modified the request to sell Bitcoin on US market (which they did NOT own)
- Expected: Error message
- **Actual Result: Trade executed successfully**

**The Outcome:**
- $1,060 of Ethereum → Sold as $43,000 of Bitcoin
- Researcher posted on X.com about the "potentially market nuking" vulnerability
- CEO responded directly
- Market was shut down
- Issue fixed within approximately one day

#### Root Cause Analysis

**Official Statement from Coinbase:**
"Missing logic validation check in their Brokerage API endpoint"

**What This Means:**
- Application validated: ✓ Price
- Application validated: ✓ Quantity  
- Application validated: ✗ Asset ID (Ethereum vs Bitcoin)
- **The system assumed the user owned whatever asset they were trying to sell**

#### Key Takeaway: UI is NOT Security

**Critical Lesson:**
> Your UI is not part of security.

- The UI prevented this type of manipulation
- The UI had proper controls in place
- **BUT**: Attackers can bypass the UI entirely
- At the API layer, the vulnerability was fully exploitable
- UI often acts as a "band-aid" covering weak or missing logic
- **Security must be implemented at the API layer**

---

### Real-World Example #2: Peloton Data Exposure

#### The Discovery
A security researcher found multiple APIs in the Peloton application that were unsecured.

#### Initial Vulnerability
- Multiple API endpoints were **completely unsecured**
- No credentials required to query these APIs
- One endpoint provided access to the **entire 4 million user database**
- Researcher notified Peloton

#### Peloton's Fix (Incomplete)
**What They Fixed:**
- Added authentication requirements
- APIs now required valid credentials
- Anonymous queries no longer allowed

**What They Missed:**
- Anyone could create a Peloton account
- Those valid credentials still allowed access to all 4 million user records
- **Authorization was still broken**

#### Authentication vs. Authorization

| Security Aspect | Question Being Asked | Peloton's Status |
|----------------|---------------------|------------------|
| **Authentication** | "Is Dan actually Dan?" | ✓ Fixed |
| **Authorization** | "Can Dan access other users' records?" | ✗ Still Broken |

**The Problem:**
- Authentication confirms identity
- Authorization determines access rights
- Peloton fixed authentication but ignored authorization
- Result: Authenticated users could still access unauthorized data

---

### Why BOLA is Critical

Both Coinbase and Peloton examples demonstrate:
1. **High Risk**: Massive data exposure and fraudulent transactions possible
2. **Common Occurrence**: Even major companies with security teams miss this
3. **Difficult Detection**: Hard to catch in testing or runtime monitoring
4. **Significant Impact**: Affects millions of users and financial transactions

---

### Best Practices for Preventing BOLA

#### 1. Shift Security Left

**Design Phase:**
- Include security team from the beginning
- Security should be "at the whiteboard"
- Integrate security concerns into product requirements
- Don't treat security as an afterthought

#### 2. Review Requirements Thoroughly

**Key Questions:**
- What data will the APIs access?
- What objects will users be able to manipulate?
- Who should have access to what?
- What are the authorization rules?

#### 3. Implement Proper Authorization Controls

**During Development:**
- Build authorization logic into the API layer
- Don't rely on UI for security
- Validate object ownership on every request
- Check user permissions before granting access

**Authorization Checklist:**
- ✓ Verify user identity (authentication)
- ✓ Verify user permissions (authorization)
- ✓ Validate object ownership
- ✓ Check access rights for specific actions
- ✓ Implement least privilege principle

#### 4. Enforce and Test Controls

**Testing Requirements:**
- Test authorization logic thoroughly
- Attempt cross-account access during testing
- Try to access unauthorized objects
- Validate that controls work as designed
- Test with different user roles and permissions

#### 5. Understand Runtime Limitations

**Important Note:**
> These authorization flaws cannot be effectively addressed by:
> - Web Application Firewalls (WAF)
> - Runtime security tools alone
> - Post-deployment patches

**Why?**
- WAFs don't understand business logic
- Runtime tools can't validate ownership rules
- These controls must be built into the application

#### 6. Implement Defense in Depth

**Multi-Layer Approach:**
1. **API Design**: Build authorization into API contracts
2. **Code Level**: Validate authorization in every function
3. **Database Level**: Use row-level security where possible
4. **Monitoring**: Log and alert on authorization failures
5. **Testing**: Regular security testing and code reviews

---

### Summary

**BOLA at a Glance:**
- **Risk Level**: Critical (Ranked #1)
- **Common Causes**: Missing authorization checks, relying on UI security
- **Impact**: Data breaches, unauthorized transactions, privacy violations
- **Prevention**: Shift-left security, proper authorization logic, thorough testing
- **Key Principle**: Security must be implemented at the API layer, not just the UI

**Remember:**
> "Your UI is not part of security" - Authorization must be enforced at the API level for every request.

---

*Note: This section covers OWASP API Security Risk #1. Additional risks will be covered in subsequent sections.*

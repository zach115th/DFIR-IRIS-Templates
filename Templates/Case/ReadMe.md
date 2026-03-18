# DFIR-IRIS Templates

A collection of **DFIR-IRIS case templates** designed to accelerate incident intake, triage, investigation, containment, remediation, recovery, and post-incident documentation.

These templates are intended to provide a structured starting point for common incident types and can be customized to fit your environment, workflows, legal requirements, reporting requirements, and case-management style.

---

## Included Templates

### 💼 Business Email Compromise
**File:** `BEC.json`

A template for suspected or confirmed business email compromise incidents involving account takeover, email impersonation, fraudulent payment requests, payroll diversion, or vendor fraud. Covers BEC validation and classification, account compromise assessment, malicious inbox rule identification, email thread and communication analysis, financial fraud risk assessment, identity remediation, and fraud notification decisions.

---

### ☁️ Cloud Data Breach
**File:** `CloudDataBreach.json`

A template for suspected or confirmed cloud data exposure or breach incidents across cloud-hosted services, platforms, tenants, or storage environments. Covers breach validation and classification, stakeholder and provider coordination, affected tenant and service scoping, cloud evidence preservation, exposure versus confirmed access assessment, identity and IAM investigation, root cause analysis, containment of sessions and resources, credential and secret remediation, configuration and sharing fixes, notification obligations, and post-incident cloud security improvements.

**Note directories:** Incident Overview · Cloud Environment · Data and Exposure · Technical Investigation · Containment and Remediation · Communications and Compliance · Post-Incident

---

### 🌊 DDoS Attack
**File:** `DDoSAttack.json`

A template for investigating and mitigating distributed denial-of-service events affecting network, application, or service availability. Covers incident validation and classification, attack type and traffic profile characterisation (volumetric, protocol, application-layer), targeted service and source distribution analysis, reflection and amplification assessment, provider and NOC coordination, layered mitigation actions, service restoration validation, extortion and diversion threat assessment, and defense improvement recommendations.

**Note directories:** Incident Overview · Attack Characterization · Impact and Scope · Mitigation and Recovery · Investigation and Post-Incident

---

### 🗃️ Data Breach
**File:** `DataBreach.json`

A template for suspected or confirmed data breach incidents involving unauthorized access, accidental disclosure, acquisition, misuse, or exfiltration of sensitive, regulated, or confidential information. Covers breach classification, legal and privacy coordination, affected system and data scoping, data sensitivity and individual impact assessment, exposure versus confirmed access determination, exfiltration and disclosure findings, containment, credential remediation, regulatory framework applicability (GDPR, HIPAA, PCI-DSS, CCPA), individual and regulator notification decisions, and post-incident control improvements.

**Note directories:** Incident Overview · Systems and Data Scope · Technical Investigation · Containment and Remediation · Legal, Privacy, and Compliance · Post-Incident

---

### 🕵️ Insider Threat
**File:** `InsiderThreat.json`

A template for investigating suspected insider activity involving misuse of access, unauthorized data handling, policy violations, or other actions by an internal user, contractor, or trusted third party. Covers allegation validation, stakeholder coordination (HR, legal, management), subject profiling and trigger event assessment, account and physical access review, technical evidence collection across file activity, email, web and cloud transfer, authentication, and removable media, evidence chain of custody, intent assessment, witness and subject interviews, and recommended corrective and control improvement actions.

> **Note:** This template contains sensitive personnel information. Access should be restricted to authorized investigators, HR, legal, and management on a need-to-know basis.

**Note directories:** Incident Overview · Subject and Access · Technical Findings · Evidence · Interviews and Coordination · Findings and Outcome

---

### 🎣 Phishing Attack
**File:** `PhishingAttack.json`

A template for suspected or confirmed phishing incidents involving malicious email, credential harvesting, malware delivery, business email compromise (BEC), callback phishing, QR phishing, or other social engineering. Covers email validation and campaign classification, header and authentication analysis (SPF/DKIM/DMARC), sender and domain infrastructure analysis, lure theme documentation, URL and landing page analysis, attachment and payload analysis, IOC extraction, recipient scoping, user interaction tracking, account compromise assessment, BEC and fraud risk evaluation, message removal and blocking, account and endpoint remediation, and awareness improvement recommendations.

**Note directories:** Incident Overview · Email and Delivery Analysis · Payload and Infrastructure · Scope and Impact · Containment and Remediation · Communications and Closure

---

### 🔒 Ransomware Attack
**File:** `RansomwareAttack.json`

A comprehensive template for suspected or confirmed ransomware incidents. Covers triage and validation, incident communications, scope assessment, evidence preservation, containment, initial access investigation, privilege escalation and lateral movement, data exfiltration and extortion risk, ransomware artifact analysis, IOC extraction, eradication, backup validation, recovery, external notification obligations, control hardening, and lessons learned.

**Note directories:** Incident Overview · Technical Investigation · Affected Environment · Response Actions · Communications and Reporting · Post-Incident

---

### 🔑 Unauthorized Access / Intrusion
**File:** `UnauthorizedAccessIntrusion.json`

A template for suspected or confirmed unauthorized access or intrusion incidents involving compromise of systems, accounts, applications, services, or infrastructure. Covers intrusion validation, affected system and identity scoping, attacker external infrastructure tracking, initial access investigation, persistence and privilege escalation analysis, lateral movement and execution findings, data access and exfiltration assessment, host isolation and containment, credential remediation, eradication of malicious artifacts and footholds, recovery validation with enhanced monitoring, legal and notification obligations, and post-incident hardening prioritised by observed attacker techniques.

**Note directories:** Incident Overview · Affected Environment · Technical Investigation · Evidence · Containment and Remediation · Impact and Reporting · Post-Incident

---

### 🌐 Web Application Compromise
**File:** `WebApplicationCompromise.json`

A template for suspected or confirmed web application compromise incidents involving exploitation of public-facing applications, APIs, web servers, middleware, plugins, CMS platforms, or related services. Covers incident validation and classification, application and component scoping (including CI/CD pipeline involvement), exploitation path analysis with raw request documentation, CVE and vulnerability referencing, web shell and malicious artifact identification, authentication and admin activity review, data and downstream system impact assessment, WAF and containment actions, application integrity validation, dependency and plugin update tracking, responsible disclosure considerations, and secure development improvement recommendations.

**Note directories:** Incident Overview · Application and Environment Scope · Technical Investigation · Containment and Remediation · Impact and Communications · Post-Incident

---

## MISP / CERT-XLM Compatibility

These templates are designed to be **MISP-friendly** and can be used with **MISP machine tags**, including **CERT-XLM** taxonomy values.

This means the templates can be aligned with tagging schemes such as:

- `tlp:amber`
- `CERT-XLM:intrusion="application-compromise"`
- `CERT-XLM:information-content-security="Unauthorised-information-access"`
- `CERT-XLM:availability="ddos"`
- `CERT-XLM:malicious-code="ransomware"`
- `CERT-XLM:fraud="phishing"`

This is especially useful if you are integrating:

- **DFIR-IRIS**
- **MISP**
- **n8n**
- or other automation workflows that sync case context, classifications, and tags into MISP events

### Important Note

Some templates are intentionally written so they can be mapped to **default MISP taxonomies**, especially **CERT-XLM**, **TLP**, and **workflow** tags.

However, successful tagging in MISP depends on your instance having the relevant taxonomies enabled and available. If a machine tag does not already exist in your MISP instance, automated tag assignment may fail until that taxonomy is enabled or refreshed.

---

## Template Structure

Each template follows a consistent JSON structure compatible with DFIR-IRIS case template import:

```json
{
  "name": "TemplateName",
  "display_name": "Human-readable Name",
  "description": "...",
  "author": "Zachary Carter",
  "title_prefix": "[PREFIX]",
  "summary": "Pre-filled case summary with placeholder fields.",
  "tags": ["tlp:amber", "..."],
  "tasks": [ { "title": "...", "description": "...", "tags": [] } ],
  "note_directories": [
    {
      "title": "Directory Name",
      "notes": [
        { "title": "Note title", "content": "## Markdown content..." }
      ]
    }
  ],
  "classification": "..."
}
```

### Note Conventions

All notes follow a consistent markdown framework:

- `##` section headers with `---` horizontal rule separators
- `<!-- HTML comment placeholders -->` for analyst-populated fields
- Bold metadata fields at the top of each note (`**Last updated:**`, `**Status:**`, etc.)
- Structured tables with context-appropriate columns for all inventory, log, and tracking data
- `- [ ]` checklist items in status and closure notes
- Open Questions sections at the end of investigation notes to track unresolved items

---

## What These Templates Provide

Each template is designed to give you a repeatable case structure with:

- A case name, display name, summary, and classification
- Recommended default tags
- A task list aligned to the incident type
- Fully structured note directories with markdown frameworks to support investigation and reporting
- A consistent and defensible response workflow

---

## Why Use These Templates

Using case templates in DFIR-IRIS helps:

- standardize investigations across analysts
- reduce case setup time
- improve documentation consistency
- make scoping and containment tasks easier to track
- support better executive summaries and final reporting
- align response actions to the type of incident being investigated

---

## Recommended Use

These templates are meant to be a **starting point**, not a hard rule.

You should review and adapt them for your environment, including:

- internal escalation paths
- legal / privacy / compliance requirements
- reporting obligations
- evidence handling and retention standards
- cloud, identity, and infrastructure specifics
- local tagging conventions
- integration with MISP, n8n, SIEM, EDR, ticketing, and notification workflows

---

## Importing into DFIR-IRIS

Import methods may vary depending on your DFIR-IRIS version and workflow, but the general approach is:

1. Download the desired JSON template file from the `Templates/` directory.
2. Open your DFIR-IRIS administration or case-template management area.
3. Create a new template or import the JSON if your deployment supports import.
4. Review the tasks, note directories, tags, and classification.
5. Save and test by creating a new case from the template.

Before production use, validate that:

- classifications match your internal taxonomy
- tags match your tagging standard
- task ordering fits your IR process
- required stakeholders are represented
- note sections match your reporting needs

---

## Suggested Workflow

A practical approach is:

- use these templates as your baseline
- clone and tailor them for your organization
- version-control changes in GitHub
- test them in DFIR-IRIS before operational rollout
- refine them after real incidents and lessons learned

---

## Template Design Philosophy

These templates are built to be:

- operationally useful
- investigation-oriented
- easy to customize
- broad enough for common DFIR use cases
- detailed enough to support repeatable response

In general, the templates try to separate:

- validation and triage
- scoping
- evidence preservation
- technical investigation
- containment and remediation
- communications and reporting
- lessons learned and closure

---

## Customization Ideas

You may want to extend these templates with:

- organization-specific severity fields
- internal contact notes
- law enforcement / regulator decision points
- insurance notification steps
- links to SOPs or playbooks
- MISP-friendly machine tags
- automation hooks for n8n
- customer notification placeholders
- executive summary scaffolding

---

## Repository Structure

```text
Templates/
├── BEC.json
├── CloudDataBreach.json
├── DDoSAttack.json
├── DataBreach.json
├── InsiderThreat.json
├── PhishingAttack.json
├── RansomwareAttack.json
├── UnauthorizedAccessIntrusion.json
└── WebApplicationCompromise.json
```

---

## Author

**Zachary Carter**

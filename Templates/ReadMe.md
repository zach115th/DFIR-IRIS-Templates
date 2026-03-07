# DFIR-IRIS Templates

A collection of **DFIR-IRIS case templates** designed to accelerate incident intake, triage, investigation, containment, remediation, recovery, and post-incident documentation.

These templates are intended to provide a structured starting point for common incident types and can be customized to fit your environment, workflows, legal requirements, reporting requirements, and case-management style.

## Included Templates

This repository currently includes the following templates in the `Templates/` directory:

- `BEC.json`
- `CloudDataBreach.json`
- `DDoSAttack.json`
- `DataBreach.json`
- `InsiderThreat.json`
- `PhishingAttack.json`
- `RansomwareAttack.json`
- `UnauthorizedAccessIntrusion.json`
- `WebApplicationCompromise.json`

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

## What These Templates Provide

Each template is designed to give you a repeatable case structure with:

- A case name, display name, summary, and classification
- Recommended default tags
- A task list aligned to the incident type
- Note directories to support investigation and reporting
- A more structured and defensible response workflow

The current template set covers:

- Business Email Compromise
- Cloud Data Breach
- DDoS Attack
- General Data Breach
- Insider Threat
- Phishing Attack
- Ransomware Attack
- Unauthorized Access / Intrusion
- Web Application Compromise

## Why Use These Templates

Using case templates in DFIR-IRIS helps:

- standardize investigations across analysts
- reduce case setup time
- improve documentation consistency
- make scoping and containment tasks easier to track
- support better executive summaries and final reporting
- align response actions to the type of incident being investigated

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

## Suggested Workflow

A practical approach is:

- use these templates as your baseline
- clone and tailor them for your organization
- version-control changes in GitHub
- test them in DFIR-IRIS before operational rollout
- refine them after real incidents and lessons learned

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

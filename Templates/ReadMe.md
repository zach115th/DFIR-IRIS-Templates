# DFIR-IRIS Templates

A collection of **DFIR-IRIS case templates** designed to accelerate incident intake, triage, investigation, containment, remediation, recovery, and post-incident documentation.

These templates are intended to provide a structured starting point for common incident types and can be customized to fit your environment, workflows, legal requirements, reporting requirements, and case-management style.

## Included Templates

This repository currently includes the following templates in the `Templates/` directory: :contentReference[oaicite:1]{index=1}

- `BEC.json`
- `CloudDataBreach.json`
- `DDoSAttack.json`
- `DataBreach.json`
- `InsiderThreat.json`
- `PhishingAttack.json`
- `RansomwareAttack.json`
- `UnauthorizedAccessIntrusion.json`
- `WebApplicationCompromise.json` :contentReference[oaicite:2]{index=2}

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

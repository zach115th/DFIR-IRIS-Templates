# 📄 DFIR-IRIS Report Templates

A collection of investigation report templates for [DFIR-IRIS](https://github.com/dfir-iris/iris-web), built in `.docx` format using the IRIS Jinja2 templating engine.

Templates are designed to be generic, case-type-aligned, and ready to load via **Advanced → Report Templates** in your IRIS instance.

---

## 📁 Templates

| Template | Case Type | Format | Description |
|----------|-----------|--------|-------------|
| [`RansomwareAttack_Report_v2.docx`](./RansomwareReportTemplate.docx) | Ransomware | `.docx` | Full incident response report aligned to the Ransomware Attack case template. Covers MITRE ATT&CK analysis, CTI findings, response actions, and IOC appendices. |

---

## ✨ Features

### Dynamic Content via IRIS Variables
All templates are populated at generation time using IRIS Jinja2 variables — no manual copy-paste from case notes into the report.

Key variables used across templates:

| Variable | Description |
|----------|-------------|
| `{{ case.name }}` | Case title |
| `{{ case.description\|markdown }}` | Executive summary / case description |
| `{{ case.open_date }}` / `{{ case.close_date }}` | Case dates |
| `{{ case.owner.user_name }}` | Lead analyst |
| `{{ case.client.customer_name }}` | Client / customer |
| `{{ case.tlp }}` | TLP classification, used in header and footer |
| `{{ case.owner.org_name }}` | Reporting organisation name on cover page |
| `{{ date }}` | Report generation date |
| `{{ doc_id }}` | Document ID in page header |

### Note Injection
The following sections auto-populate from matching IRIS case notes. Keep your note titles consistent with your case templates for these to render correctly.

| Report Section | Note Title (must match exactly) |
|----------------|---------------------------------|
| §2.2 How the Incident Was Identified | `Initial summary` |
| §2.3 Business Impact | `Business impact` |
| §5 Ransomware Variant and Behavior | `Ransomware variant and behavior` |
| §6 Cyber Threat Intelligence | `Cyber Threat Intelligence` |

### Conditional Logic
Templates include smart rendering logic that responds to the state of your case data:

- **⚠ Exfiltration Warning Banner** — A red callout box appears at the top of Section 2 automatically if any IOC in the case carries the tag `exfiltration`. Prompts analysts to assess regulatory notification obligations before the report is finalised.

- **⏳ Open Tasks Tracker** — If any case tasks remain in a non-`Closed` state when the report is generated, a blue callout and task table render before Section 7 (Response Actions), listing all outstanding items with their status and last update date.

- **Compromised Asset Detail Blocks** — Appendix A renders a dedicated sub-section for each asset marked as compromised, including its full description and a table of linked IOCs. If no assets are compromised, a green all-clear callout is shown instead.

- **Empty-State Guards** — Appendices A through D check whether their respective data lists (assets, IOCs, evidence, timeline) contain any records. If a list is empty, a neutral placeholder callout is rendered rather than an empty section heading.

- **IOC Type Grouping** — Appendix B automatically splits IOCs into three sub-tables: Network Indicators (IPs, domains, URLs), File Indicators (hashes, filenames), and Other Indicators (email addresses, accounts, etc.), based on the IOC type name assigned in IRIS.

---

## 🗂 Companion Case Templates

These report templates are designed to work alongside the case templates in [`/Templates/Case`](../Case/). Note injection and section structure assume the note titles defined in those case templates are present and populated.

| Report Template | Companion Case Template |
|----------------|------------------------|
| `RansomwareReportTemplate.docx` | `RansomwareAttack` |

---

## 🚀 Installation

1. In your IRIS instance, navigate to **Advanced → Report Templates**
2. Click **Add a template**
3. Upload the `.docx` file and set the type to **Investigation**
4. Save — the template will now appear in **Reports** within any case

To generate a report, open a case and go to **Reports → Generate**, then select the template.

> **Note:** IRIS report templates require Admin role to manage. Report generation is available to all users with case access.

---

## 🛠 Template Development

Templates are built using [docx-js](https://github.com/dolanmiu/docx) and use the [IRIS Jinja2 templating engine](https://docs.dfir-iris.org/operations/reports/) at render time.

### Available IRIS Template Variables

Full reference: [docs.dfir-iris.org/operations/reports](https://docs.dfir-iris.org/operations/reports/)

**Lists** (use `{%tr for item in list %}` inside tables, `{% for item in list %}` in body text):

| Variable | Attributes |
|----------|-----------|
| `assets` | `asset_name`, `asset_ip`, `type`, `asset_description`, `asset_compromise_status`, `compromised`, `asset_ioc` |
| `iocs` | `ioc_value`, `ioc_description`, `ioc_type.type_name`, `ioc_tags` |
| `notes` | `note_title`, `note_content`, `note_creationdate`, `note_lastupdate` |
| `tasks` | `task_title`, `task_description`, `task_status`, `task_open_date`, `task_last_update`, `task_close_date`, `task_tags` |
| `timeline` | `event_date`, `event_title`, `event_content`, `event_source`, `category`, `event_tags`, `assets` |
| `evidences` | `filename`, `date_added`, `file_hash`, `added_by` |

### Key Templating Patterns

**Conditional section (only renders if list is non-empty):**
```jinja
{% if assets|count %}
  ... content ...
{% else %}
  No assets recorded.
{% endif %}
```

**Table loop:**
```jinja
{%tr for ioc in iocs %}
  {{ ioc.ioc_value }}   {{ ioc.ioc_type.type_name }}   {{ ioc.ioc_description }}
{%tr endfor %}
```

**Note injection by title:**
```jinja
{% for note in notes %}{% if note.note_title == "Initial summary" %}
  {{ note.note_content|markdown }}
{% endif %}{% endfor %}
```

**Filter compromised assets only:**
```jinja
{% for asset in assets %}{% if asset.compromised %}
  {{ asset.asset_name }}
{% endif %}{% endfor %}
```

**Filter open tasks only:**
```jinja
{%tr for task in tasks|rejectattr('task_status', 'equalto', 'Closed')|list %}
  {{ task.task_title }}   {{ task.task_status }}
{%tr endfor %}
```

> **Tip:** Jinja2 control tags (`{% if %}`, `{% for %}`, `{% endif %}`) embedded in `.docx` templates must be placed inside table cells or paragraph runs. Wrap them in 1pt white text to keep them invisible in the rendered output but parseable by IRIS.

---

## 📋 Report Structure (Ransomware Template)

| Section | Content |
|---------|---------|
| Cover page | Case name, org, prepared for, date, lead analyst, TLP |
| Table of Contents | Auto-generated from headings |
| 1. Executive Summary | `case.description\|markdown` |
| 2. Incident Overview | Case details table, how identified (from note), business impact (from note), analysis timeline |
| 3. Scope | Affected systems (asset loop), affected accounts |
| 4. MITRE ATT&CK Analysis | TA0001–TA0040 tactic tables |
| 5. Ransomware Variant | Variant ID table, malware artifacts (from note) |
| 6. CTI Findings | Threat actor profile, intelligence sources (from note) |
| 7. Response Actions | Open tasks callout (conditional), containment, eradication, recovery |
| 8. Remediation | Immediate actions, strategic improvements |
| 9. Conclusion | Free-text closing summary |
| Appendix A | Asset summary table + compromised asset detail blocks (conditional) |
| Appendix B | IOCs split by type: network, file, other (conditional) |
| Appendix C | Evidence / received files (conditional) |
| Appendix D | Event timeline (conditional) |

---

## 📚 Resources

- [DFIR-IRIS Documentation](https://docs.dfir-iris.org)
- [IRIS Report Templating Reference](https://docs.dfir-iris.org/operations/reports/)
- [IRIS Case Templates Reference](https://docs.dfir-iris.org/operations/case_templates/)
- [DFIR-IRIS on GitHub](https://github.com/dfir-iris/iris-web)
- [TLP Definitions (CISA)](https://www.cisa.gov/tlp)
- [MITRE ATT&CK Framework](https://attack.mitre.org)

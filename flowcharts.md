# Vulnrichment flowcharts

This is the flowchart for processing [new CVE Records](assets/flowcharts.md-1.png). 

```mermaid
---
title: "CISA Vulnrichment: New CVE Record (2024-12-29)"
---
flowchart TD
    new_CVE@{ shape: stadium, label: "New CVE"}
    add_SSVC@{ shape: rect, label: "Add SSVC" }
    fork@{ shape: fork }
    on_KEV@{ shape: diamond, label: "On KEV?" }
    add_KEV@{ shape: rectangle, label: "Add KEV \n SSVC E:A" }
    cna_CVSS@{ shape: diamond, label: "CNA \n provides \n CVSS?" }
    add_CVSS@{ shape: rectangle, label: "Add CVSS" }
    cna_CWE@{ shape: diamond, label: "CNA \n provides \n CWE?" }
    add_CWE@{ shape: rectangle, label: "Add CWE" }
    new_refs@{ shape: diamond, label: "Additional \n references?" }
    add_refs@{ shape: rectangle, label: "Add \n references"}
    join@{ shape: join }
    publish@{ shape: rectangle, label: "Publish" }
    adp@{ shape: rectangle, label: "CVE ADP" }
    github@{ shape: rectangle, label: "GitHub" }
    done@{ shape: stadium, label: "Done"}
    new_CVE --> add_SSVC
    add_SSVC --> fork
    fork --> on_KEV
    fork --> cna_CVSS
    fork --> cna_CWE
    fork --> new_refs
    on_KEV --> | Yes | add_KEV
    add_KEV --> join
    on_KEV --> | No | join
    cna_CVSS --> | Yes | join
    cna_CVSS --> | No | add_CVSS
    add_CVSS --> join
    cna_CWE --> | Yes | join
    cna_CWE --> | No | add_CWE
    add_CWE --> join
    new_refs --> | Yes | add_refs
    add_refs --> join
    new_refs --> | No | join
    join --> publish
    publish --> adp
    publish --> github
    adp --> done
    github --> done
```

This is the flowchart for processing [updated CVE Records](assets/flowcharts.md-2.png).

```mermaid
---
title: "CISA Vulnrichment: Updated CVE Record (2024-12-29)"
---
flowchart TD
    updated_CVE@{ shape: stadium, label: "Updated CVE" }
    change@{ shape: diamond, label: "Material \n change?" }
    ssvc@{ shape: diamond, label: "Update SSVC?" }
    update_SSVC@{ shape: rect, label: "Update SSVC" }
    fork@{ shape: fork }
    on_KEV@{ shape: diamond, label: "On KEV?" }
    add_KEV@{ shape: rectangle, label: "Add KEV \n SSVC E:A" }
    cna_CVSS@{ shape: diamond, label: "CNA \n provides \n CVSS?" }
    remove_CVSS@{ shape: rectangle, label: "Remove CVSS" }
    cvss@{ shape: diamond, label: "Update CVSS?" }
    update_CVSS@{ shape: rect, label: "Update CVSS" }
    cna_CWE@{ shape: diamond, label: "CNA \n provides \n CWE?" }
    remove_CWE@{ shape: rectangle, label: "Remove CWE" }
    cwe@{ shape: diamond, label: "Update CWE?" }
    update_CWE@{ shape: rect, label: "Update CWE" }
    refs@{ shape: diamond, label: "Update \n references?" }
    update_refs@{ shape: rectangle, label: "Update \n references"}
    join@{ shape: join }
    publish@{ shape: rectangle, label: "Publish" }
    adp@{ shape: rectangle, label: "CVE ADP" }
    github@{ shape: rectangle, label: "GitHub" }
    done@{ shape: stadium, label: "Done"}
    updated_CVE --> change
    change --> | No | done
    change --> | Yes | fork
    fork --> ssvc
    fork --> on_KEV
    fork --> cna_CVSS
    fork --> cna_CWE
    fork --> refs
    ssvc --> | Yes | update_SSVC
    update_SSVC --> join
    ssvc --> | No | join
    on_KEV --> | Yes | add_KEV
    add_KEV --> join
    on_KEV --> | No | join
    cna_CVSS --> | Yes | remove_CVSS
    remove_CVSS --> join
    cna_CVSS --> | No | cvss
    cvss --> | Yes | update_CVSS
    update_CVSS --> join
    cvss --> | No | join
    cna_CWE --> | Yes | remove_CWE
    remove_CWE --> join
    cna_CWE --> | No | cwe
    cwe --> | Yes | update_CWE
    update_CWE --> join
    cwe --> | No | join
    refs --> | Yes | update_refs
    update_refs --> join
    refs --> | No | join
    join --> publish
    publish --> adp
    publish --> github
    adp --> done
    github --> done
```

To generate images use `mermaid-cli`.

```
npm install -g @mermaid-js/mermaid-cli
mmdc -i flowcharts.md -t neutral -e png -s 2
```

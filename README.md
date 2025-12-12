# IBM SOAR AppHost Installation Guide

This repository provides a **step-by-step SOP** for installing and pairing an
**IBM Resilient (SOAR) AppHost** using a virtual appliance (OVA).

---
### Pre-Requisites

| Requirement | Details |
|------------|--------|
| SOAR Version | 51.0.6.2.23 |
| Deployment Type | Virtual Appliance (OVA) |
| Files | `apphost-1.15.5.0.2.ova` / `ova` |
| Hardware | As per IBM sizing documentation |
| FQDN | `soarapp.<yourdomain>` |
| Ports | 443, 65000, 65001 |

**Important:** Values inside `< >` must be replaced with environment-specific values before execution.


📘 Full installation guide:  
➡️ [`docs/installation/apphost-installation.md`](docs/installation/apphost-installation.md)

## Scope
- AppHost OVA deployment
- SOAR pairing
- Kubernetes pod verification

## Audience
- SOC Engineers
- SOAR Administrators
- Security Platform Engineers

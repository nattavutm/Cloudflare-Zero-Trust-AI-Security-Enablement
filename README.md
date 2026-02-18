# Cloudflare Zero Trust Workshop - AI Security

Hands-on lab workshop: Deploy Cloudflare Zero Trust to protect employees from unauthorized external AI services.

## Key Technologies
- **Zero Trust Network Access (ZTNA)**
- **Secure Web Gateway (SWG)**
- **Data Loss Prevention (DLP)**
- **Cloudflare Browser Isolation (RBI)**

## Architecture Overview

```
┌─────────────────┐
│   Employees     │
│  (Any Device)   │
└────────┬────────┘
         │
         ├─── WARP Client (Secure Tunnel)
         │
┌────────▼────────────────────────┐
│   Cloudflare Zero Trust         │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Identity & Context       │  │
│  │  - Identity Provider (IdP)│  │
│  │  - Device Posture Checks  │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Secure Web Gateway (SWG) │  │
│  │  - Application Control    │  │
│  │  - DLP Scanning           │  │
│  │  - Browser Isolation      │  │
│  └───────────────────────────┘  │
│                                 │
│  ┌───────────────────────────┐  │
│  │  Analytics & Logging      │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
         │
         ├─── ✅ Approved AI (Isolated)
         └─── ❌ Blocked AI Services

```

## What You'll Build

- **Module 1:** Initialize a Cloudflare Zero Trust environment, configure your org and auth, and onboard devices with WARP
- **Module 2:** Use Secure Web Gateway to discover and block unapproved AI applications and protect AI prompts
- **Module 3:** Build Data Loss Prevention (DLP) policies to protect sensitive data in AI interactions
- **Module 4:** Provide secure, approved AI access with Cloudflare Browser Isolation (RBI)
- **Module 5:** Use CASB integrations with OpenAI and Anthropic to continuously monitor AI SaaS posture

## Workshop Modules

| Module | Lab |
|--------|-----|
| 1 | [Zero Trust Setup](./docs/01-zerotrust-setup.md) |
| 2 | [Block AI Services](./docs/02-block-ai-services.md) |
| 3 | [Data Loss Prevention](./docs/03-dlp-policies.md) |
| 4 | [Approved AI Access with RBI](./docs/05-approved-access.md) |
| 5 | [CASB for OpenAI & Anthropic](./docs/06-casb-ai-integrations.md) |

> Optional: [Monitoring & Analytics](./docs/04-monitoring.md) for Gateway and DLP visibility.

## Detailed Learning Path

### Module 1: Zero Trust Setup
- [Initialize Cloudflare Zero Trust](./docs/01-zerotrust-setup.md)
- [Configure organization and authentication settings](./docs/01-zerotrust-setup.md)
- [Deploy and connect the WARP client](./docs/01-zerotrust-setup.md)
- [Verify device connectivity and enrollment](./docs/01-zerotrust-setup.md)

### Module 2: Block AI Services
- [Create HTTP filtering policies](./docs/02-block-ai-services.md)
- [Test blocking rules](./docs/02-block-ai-services.md)
- [AI prompt protection for web-based AI apps](./docs/02-block-ai-services.md)
- [Gateway HTTP redirects + Workers block pages](./docs/02-block-ai-services.md)

### Module 3: Data Loss Prevention
- [Create and customize DLP profiles](./docs/03-dlp-policies.md)
- [Configure sensitive data patterns (PII, Financial, etc.)](./docs/03-dlp-policies.md)
- [Apply DLP scanning to AI service uploads](./docs/03-dlp-policies.md)
- [Prompt topics](./docs/03-dlp-policies.md)
- [Detection entries – Exact Data Match (EDM)](./docs/03-dlp-policies.md)
- [Detection entries – Custom Wordlists (CWL)](./docs/03-dlp-policies.md)

### Module 4: Approved AI Access with RBI
- [Define allowlist policies for approved AI tools](./docs/05-approved-access.md)
- [Configure Cloudflare Remote Browser Isolation (RBI)](./docs/05-approved-access.md)
- [Implement identity-based and time-based access](./docs/05-approved-access.md)
- [Verify the secure isolation environment](./docs/05-approved-access.md)

### Module 5: CASB
- [Integrate CASB with OpenAI and Anthropic](./docs/06-casb-ai-integrations.md)

## Troubleshooting

### WARP Client Connectivity
```bash
# Check current WARP status
warp-cli status

# Reset registration if needed
warp-cli registration delete
warp-cli registration new

# Connect to the Zero Trust fabric
warp-cli connect
```

## Resources

- [Cloudflare Zero Trust Dashboard](https://one.dash.cloudflare.com)
- [Zero Trust Documentation](https://developers.cloudflare.com/cloudflare-one/)
- [Gateway Filtering Policies](https://developers.cloudflare.com/cloudflare-one/policies/filtering/)
- [Cloudflare Browser Isolation](https://developers.cloudflare.com/cloudflare-one/policies/browser-isolation/)

---


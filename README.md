# Cloudflare Zero Trust Workshop - AI Security

Hands-on lab workshop: Deploy Cloudflare Zero Trust to protect employees from unauthorized external AI services.

## Key Technologies
- **Zero Trust Network Access (ZTNA)**
- **Secure Web Gateway (SWG)**
- **Data Loss Prevention (DLP)**
- **Cloudflare Browser Isolation**

## What You'll Build

- **Lab 1:** Setup Zero Trust environment and connect devices
- **Lab 2:** Configure Gateway policies to block unauthorized AI services
- **Lab 3:** Implement Data Loss Prevention (DLP) for AI tools
- **Lab 4:** Setup monitoring, alerts, and analytics
- **Lab 5:** Create approved AI access with Browser Isolation

## Workshop Modules

| Module | Lab | Duration |
|--------|-----|----------|
| 1 | [Zero Trust Setup](./docs/01-zerotrust-setup.md) | 20 min |
| 2 | [Block AI Services](./docs/02-block-ai-services.md) | 30 min |
| 3 | [Data Loss Prevention](./docs/03-dlp-policies.md) | 30 min |
| 4 | [Monitoring & Analytics](./docs/04-monitoring.md) | 20 min |
| 5 | [Approved AI Access](./docs/05-approved-access.md) | 30 min |

**Total Estimated Time:** 2 hours 10 minutes

## Objectives

By the end of this workshop, you will be able to:
- ✅ Deploy Cloudflare Zero Trust using the WARP client
- ✅ Block access to unauthorized AI services (ChatGPT, Claude, Gemini, etc.)
- ✅ Prevent sensitive data uploads to public AI tools using DLP
- ✅ Configure identity-based access controls and device posture checks
- ✅ Create an allowlist for approved corporate AI services
- ✅ Monitor and analyze real-time AI service usage
- ✅ Configure automated alerts for policy violations
- ✅ Leverage Browser Isolation for secure access to approved AI tools

## Pre-requirements (Before the Workshop)

To get the most out of this hands-on lab, please complete these steps **before** the session:
1. **Cloudflare Account**: [Sign up](https://dash.cloudflare.com/sign-up) for a free account if you don't have one.
2. **Account Verification**: Ensure your email is verified (check your inbox for a verification link).
3. **Local Admin Rights**: Ensure you have permission to install software (Cloudflare WARP) on your computer.
4. **Mobile Device**: Have a smartphone ready for Email OTP or 2FA authentication.

## System Requirements

## Architecture Overview

```text
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
│  ┌───────────────────────────┐ │
│  │  Identity & Context       │ │
│  │  - Identity Provider (IdP) │ │
│  │  - Device Posture Checks  │ │
│  └───────────────────────────┘ │
│                                 │
│  ┌───────────────────────────┐ │
│  │  Secure Web Gateway (SWG) │ │
│  │  - Application Control    │ │
│  │  - DLP Scanning           │ │
│  │  - Browser Isolation      │ │
│  └───────────────────────────┘ │
│                                 │
│  ┌───────────────────────────┐ │
│  │  Analytics & Logging      │ │
│  └───────────────────────────┘ │
└─────────────────────────────────┘
         │
         ├─── ✅ Approved AI (Isolated)
         └─── ❌ Blocked AI Services
```

## Quick Start

1. Start with [Module 1: Zero Trust Setup](./docs/01-zerotrust-setup.md)
2. Continue to [Module 2: Block AI Services](./docs/02-block-ai-services.md)
3. Complete [Module 3: Data Loss Prevention](./docs/03-dlp-policies.md)
4. Setup [Module 4: Monitoring & Analytics](./docs/04-monitoring.md)
5. Finish with [Module 5: Approved AI Access](./docs/05-approved-access.md)

## AI Services Blocked by Default

### Chat AI Services
- `chatgpt.com` / `chat.openai.com`
- `claude.ai` (Anthropic)
- `gemini.google.com` (Google Gemini)
- `perplexity.ai`
- `character.ai`
- `poe.com`
- `you.com`

### AI Code Assistants
- GitHub Copilot
- Microsoft Copilot
- Codeium
- Tabnine
- Cursor

### AI Image & Media Generation
- Midjourney
- Leonardo AI
- Playground AI
- GetImg AI

### AI Writing & Productivity
- Jasper
- Copy.ai
- Writesonic
- Rytr

## Detailed Learning Path

### Module 1: Zero Trust Setup (20 min)
- Initialize Cloudflare Zero Trust
- Configure organization and authentication settings
- Deploy and connect the WARP client
- Verify device connectivity and enrollment

### Module 2: Block AI Services (30 min)
- Create HTTP filtering policies
- Configure granular application-based blocking
- Implement domain-based restrictions
- Test blocking rules and view real-time logs

### Module 3: Data Loss Prevention (30 min)
- Create and customize DLP profiles
- Configure sensitive data patterns (PII, Financial, etc.)
- Apply DLP scanning to AI service uploads
- Review and mitigate DLP violations

### Module 4: Monitoring & Analytics (20 min)
- Explore Gateway Analytics dashboards
- Create custom reports for AI usage
- Setup automated notifications (Email/Webhooks)
- (Optional) Export logs to a SIEM

### Module 5: Approved AI Access (30 min)
- Define allowlist policies for approved AI tools
- Configure Cloudflare Browser Isolation
- Implement identity-based and time-based access
- Verify the secure isolation environment

## Project Structure

```text
cloudflare-ai-security-workshop/
├── README.md                           # Workshop guide (This file)
├── QUICK-REFERENCE.md                  # Quick commands and links
├── docs/                               # Detailed lab instructions
│   ├── 01-zerotrust-setup.md
│   ├── 02-block-ai-services.md
│   ├── 03-dlp-policies.md
│   ├── 04-monitoring.md
│   └── 05-approved-access.md
├── configs/                            # Configuration templates
│   ├── gateway-policies.json
│   ├── dlp-profiles.json
│   └── warp-config.xml
└── scripts/                            # Helper scripts
    ├── deploy-policies.sh
    └── test-blocking.sh
```

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

### Policy Issues
- **Precedence:** Ensure rules are ordered correctly (lower number = higher priority).
- **Scope:** Verify the user is not in an exclusion group.
- **Connectivity:** Ensure the device is successfully connected to the WARP client.
- **Logs:** Review Gateway logs for specific policy match reasons.

## Resources

- [Cloudflare Zero Trust Dashboard](https://one.dash.cloudflare.com)
- [Zero Trust Documentation](https://developers.cloudflare.com/cloudflare-one/)
- [Gateway Filtering Policies](https://developers.cloudflare.com/cloudflare-one/policies/filtering/)
- [Cloudflare Browser Isolation](https://developers.cloudflare.com/cloudflare-one/policies/browser-isolation/)

---

**Ready to start?** Begin with [Module 1: Zero Trust Setup](./docs/01-zerotrust-setup.md)

⭐ If this workshop helped you, please give it a star!

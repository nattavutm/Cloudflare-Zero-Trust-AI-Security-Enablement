#+ Lab 5: CASB – OpenAI & Anthropic Integrations
+
+## Introduction
+In this lab, you will use Cloudflare CASB to integrate with OpenAI and Anthropic so you can:
+
+- Discover how your organization uses AI SaaS (ChatGPT, Claude, OpenAI Platform, Anthropic API)
+- Detect misconfigurations and risky settings
+- Identify potential data exposure and DLP risks
+
+> Reference: Cloudflare docs – CASB integrations for **OpenAI** and **Anthropic**.
+
+## Prerequisites
+
+- Access to the **Cloudflare Zero Trust / One** dashboard with CASB enabled.
+- Admin-level access to:
+  - An **OpenAI** organization (e.g., ChatGPT Enterprise / OpenAI Platform).
+  - An **Anthropic** organization (Claude console / API).
+
+## Part 1: Connect the OpenAI CASB Integration
+
+1. In the Zero Trust dashboard, go to **Security Center → CASB → Integrations**.
+2. Find and select **OpenAI**.
+3. Review the integration description and required scopes.
+4. Click **Connect**:
+   - You will be redirected to OpenAI to grant Cloudflare access, or
+   - You will be asked to provide API credentials, depending on the current integration flow.
+5. Approve the requested permissions so Cloudflare can:
+   - Read configuration for your ChatGPT / OpenAI workspaces and projects.
+   - Retrieve posture and usage information.
+6. Back in the Cloudflare dashboard, confirm the integration status shows as **Connected**.
+
+## Part 2: Connect the Anthropic CASB Integration
+
+1. Still in **Security Center → CASB → Integrations**, locate **Anthropic**.
+2. Click **Connect** and review requested permissions.
+3. Follow the authorization flow:
+   - Sign in with an Anthropic admin account.
+   - Grant Cloudflare access to organization/workspace metadata and posture.
+4. Once complete, verify that the integration status changes to **Connected**.
+
+## Part 3: Review CASB Findings for AI Apps
+
+1. Navigate to **Security Center → CASB → Findings**.
+2. Filter by **Application** and select **OpenAI** and/or **Anthropic**.
+3. Review the findings categories, such as:
+   - Public or overly permissive workspaces/projects.
+   - Inactive or orphaned API keys and tokens.
+   - Risky sharing settings or external collaborators.
+4. For each high/medium severity finding:
+   - Open the details panel.
+   - Note the recommended remediation steps.
+
+## Part 4: Map CASB Findings to Zero Trust Policies
+
+1. From the findings list, identify risks that should influence access policy, for example:
+   - Users with elevated permissions in OpenAI / Anthropic.
+   - Projects with sensitive data or excessive sharing.
+2. In **Zero Trust**, adjust:
+   - **Gateway HTTP policies** to:
+     - Block or isolate risky tenants / instances.
+     - Require WARP and DLP for known AI SaaS destinations.
+   - **Identity-based rules** to:
+     - Restrict access to specific groups (e.g., security, data science).
+3. Document which CASB findings map to which Zero Trust/HTTP/DLP policies so that posture issues drive enforcement.
+
+## Lab Verification Checklist
+
+- CASB shows **OpenAI** and **Anthropic** integrations in a **Connected** state.
+- Findings are visible for at least one of the AI providers.
+- You can explain how specific CASB findings should inform:
+  - SWG HTTP/DLP policies for AI usage.
+  - Identity and device-based access controls in Zero Trust.
+

# Lab 4: Approved AI Access with RBI

## Introduction
In this lab, you will provide secure access to approved AI tools using Cloudflare Remote Browser Isolation (RBI), combining identity, device posture, and time-based controls.

> Reference: Cloudflare docs – `Browser Isolation` policies and `Secure Web Gateway` HTTP policies.

## Part 1: Define Allowlist Policies for Approved AI Tools

1. Identify the AI tools that will be **approved** (e.g., a corporate AI portal, specific ChatGPT or Claude tenants).
2. In the Zero Trust dashboard, go to **Gateway → Firewall Policies → HTTP**.
3. Create a new policy:
   - Set **Action** to **Allow** (or **Isolate** if available directly here in your plan).
   - Scope the policy to:
     - Specific **Application** entries for the AI tools, or
     - Exact **Hostnames** / **URLs** for your corporate AI portals.
4. Optionally, restrict to:
   - Specific **User groups** or **SSO groups**.
   - Devices with required **posture checks** (e.g., OS version, EDR).
5. Save the policy.

## Part 2: Configure Cloudflare Remote Browser Isolation (RBI)

1. Go to **Gateway → Firewall Policies → HTTP** (or **Browser Isolation** section, depending on your UI).
2. Create a policy with:
   - **Action**: **Isolate**.
   - **Selector**: set to match your approved AI tools (same applications or hostnames as in Part 1).
3. Configure isolation settings (if available in your plan), such as:
   - Disable **file uploads**.
   - Disable **copy/paste** from the isolated session to the local device.
   - Restrict **downloads**.
4. Ensure the **Isolate** policy is evaluated **before** any broad Allow rules for these destinations.
5. Save the policy.

## Part 3: Implement Identity-Based and Time-Based Access

1. Edit your allowlist/isolation policies for AI tools.
2. In **Selectors/Conditions**, add:
   - **User Email** or **User Group** selectors to limit access to specific teams.
   - **Device Posture** selectors (e.g., device is managed, EDR installed) to ensure only compliant devices access AI tools.
3. For time-based access (if available in your environment):
   - Use **schedule** or **time-of-day** conditions to only allow AI usage within defined business hours.
4. Save policy changes.

## Part 4: Verify the Secure Isolation Environment

1. From an approved user account on a compliant WARP-enrolled device:
   - Access the approved AI tool (e.g., corporate AI portal).
   - Confirm that the session opens in an **Isolated** browser (look for RBI banner/watermark or isolation header).
2. Attempt restricted actions:
   - Try to upload a file if uploads are disabled.
   - Try to copy content from the isolated session to your local clipboard.
3. Confirm that:
   - Restricted actions are blocked as configured.
   - Events are logged in **Gateway** and **Browser Isolation** analytics (where available).

## Lab Verification Checklist

- Only approved users/devices can reach the allowed AI tools.
- Sessions to approved AI tools are running in Cloudflare RBI.
- Copy/paste, uploads, or downloads are restricted according to policy.
- Logs show isolated AI access and any policy blocks.

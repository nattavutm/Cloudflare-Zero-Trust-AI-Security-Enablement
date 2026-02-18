# Lab 3: Data Loss Prevention (DLP)

## Introduction
In this lab, you will build Data Loss Prevention policies that:

- Create and customize DLP profiles
- Configure sensitive data patterns (PII, financial, etc.)
- Apply DLP scanning to AI service uploads
- Use prompt topics and detection entries such as Exact Data Match (EDM) and Custom Wordlists (CWL)

> Reference: Cloudflare docs – `DLP` → `Profiles`, `Detection entries`, `Exact Data Match`, and `Custom wordlists`.

## Part 1: Create and Customize DLP Profiles

1. In the Zero Trust dashboard, go to **DLP** → **Profiles**.
2. Review built-in profiles (e.g., **Payment cards**, **National IDs**).
3. Enable the profiles that are relevant to your region and use case.
4. Click **Create profile** to add a **Custom DLP profile** for your organization.
5. Give it a name such as **"AI – Corporate Secrets"** and description.

## Part 2: Configure Sensitive Data Patterns (PII, Financial, etc.)

Inside your custom profile:

1. Add **Detection entries** for:
   - **PII** (e.g., national IDs, phone numbers, email addresses).
   - **Financial** data (e.g., IBAN, internal account numbers).
2. Use available **built-in detectors** where possible to reduce maintenance.
3. Scope the profile to relevant **countries/regions** (if available) to minimize false positives.

## Part 3: Prompt Topics

Prompt topics let you flag risky **themes** in prompts, even when they do not contain specific identifiers.

1. In the same DLP profile, add a **Prompt topics** entry (name it e.g., **"AI – Sensitive Projects"**).
2. Add examples of sensitive topics such as:
   - Internal project names
   - Confidential product codenames
   - Sensitive research code names
3. Save the profile so that these topics are recognized when users try to paste prompts into AI tools.

## Part 4: Detection Entries – Exact Data Match (EDM)

Exact Data Match allows you to match specific rows from a reference dataset.

1. Prepare a small CSV dataset of **synthetic** (non-production) values for the lab (e.g., fake employee IDs).
2. In **DLP → Exact Data Match**, create a new **EDM dataset**:
   - Upload the CSV.
   - Define which column(s) are identifiers.
3. Associate this EDM dataset with your custom DLP profile.
4. Save the profile.

## Part 5: Detection Entries – Custom Wordlists (CWL)

Custom Wordlists are ideal for maintaining lists of sensitive tokens or phrases.

1. Go to **DLP → Custom Wordlists**.
2. Create a new wordlist for items like:
   - Internal environment names (`prod-eu`, `prod-us`)
   - Internal code names
   - Sensitive labels (e.g., `CONFIDENTIAL`, `INTERNAL ONLY`)
3. Link the wordlist to your DLP profile via a **Custom wordlist** detection entry.

## Part 6: Apply DLP Scanning to AI Service Uploads

Now tie DLP into your HTTP policies for AI tools.

1. Navigate to **Gateway → Firewall Policies → HTTP**.
2. Create or edit a policy that targets AI domains or applications (e.g., `chatgpt.com`, `claude.ai`, `gemini.google.com`).
3. In the **DLP** section of the policy:
   - Attach your custom DLP profile(s).
   - Choose the enforcement action:
     - **Block** for strict protection.
     - **Allow with log** for monitoring mode.
4. Scope the policy to `POST` methods and upload-related content types if you want to focus on uploads and prompts.
5. Save the policy.

## Lab Verification Checklist

1. From a WARP-enrolled device, open a web-based AI chat (e.g., ChatGPT, Claude, Gemini).
2. Test the following in prompts or uploads:
   - A **fake credit card** or PII sample → should trigger built-in/bespoke DLP entries.
   - A **synthetic ID** from your EDM dataset → should be detected by EDM.
   - A **keyword** from your custom wordlist → should be detected by CWL.
   - A **prompt containing a sensitive topic** (project name, codename) → should match your prompt topics entry.
3. Confirm in **Gateway → Logs** and **DLP logs** that:
   - The event is logged with the **matched profile and detection entry**.
   - The **action** (Block/Allow with log) matches your configuration.

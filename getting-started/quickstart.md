---
icon: bullseye-arrow
cover: ../.gitbook/assets/savebanner.jpeg
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Quickstart

Deploy your first application to the permaweb in under 5 minutes using Arlink. This guide will walk you through connecting your wallet, setting up your first deployment, and publishing your application.

## Prerequisites

Before you begin, make sure you have:

* An Arweave wallet (Wander recommended)
* A GitHub account or Protocol Land account
* Your web application code ready to deploy

## Step 1: Connect Your Wallet

1. Visit [Arlink Dashboard](https://arlink.arweave.net/)
2. Click "Connect Wallet" in the top right corner
3. Select your wallet provider (Wander recommended)
4. Authorize the connection when prompted

{% hint style="info" %}
If you don't have an Arweave wallet yet, we recommend installing [Wander](https://www.wander.app/) first.
{% endhint %}

## Step 2: Create Your First Deployment

Choose your preferred deployment method:

{% tabs %}
{% tab title="GitHub Deploy" %}
1. Click "New Deployment" in the dashboard
2. Select "Import from GitHub"
3. Authorize Arlink in GitHub if prompted
4. Choose your repository
5.  Verify your build settings (pre-filled based on repository analysis):

    ```yaml
    Project Name: my-first-app
    Branch: main
    Install Command: pnpm install  # auto-detected from package manager
    Build Command: npm run build   # auto-detected from package.json
    Output Directory: dist         # auto-detected from config
    ```

    Review these settings and adjust if needed.
{% endtab %}

{% tab title="Protocol Land Deploy" %}
1. Click "New Deployment" in the dashboard
2. Select "Import from Protocol Land"
3. Choose your repository from the list
4.  Configure your build settings:

    ```yaml
    Project Name: my-first-app
    Install Command: npm ci  # or yarn install
    Build Command: npm run build  # or yarn build
    Output Directory: dist  # or build this is where your static fiels are exported 
    ```
{% endtab %}
{% endtabs %}

## Step 3: Set Up Your Domain

Choose your preferred domain option:

{% tabs %}
{% tab title="Arlink undername " %}
1. Enable "Arlink undername" in deployment settings
2. Enter your preferred name (e.g., `myapp`)
3. Your application will be available at: `myapp_arlink.arweave.net`

{% hint style="info" %}
Custom names must be unique across Arlink. If your chosen name is taken, try adding a unique identifier.
{% endhint %}
{% endtab %}

{% tab title="Existing ArNS" %}
1. Enable "Use Existing ArNS" in deployment settings
2. Select your ArNS name from the dropdown
3. Confirm the connection

{% hint style="warning" %}
You must own or control the ArNS name to use this option.
{% endhint %}
{% endtab %}
{% endtabs %}

## Step 4: Deploy

1. Review your deployment settings.
2. Click **Deploy** to initiate the build process.
3. Monitor the build progress in real-time.
4. Once complete, you'll see a success card—use it to visit your deployment and access the deployment management panel.

<details>

<summary>What happens during deployment?</summary>

1. Your code is cloned from the repository
2. Dependencies are installed using your specified install command
3. Application is built using your build command
4. Built files are bundled and uploaded to Arweave
5. ArNS records are updated (if configured)
6. Your application becomes available on the permaweb

</details>

## Common Questions

<details>

<summary>How much does deployment cost?</summary>

Deployment costs are currently subsidized during our promotional beta. Please note that this subsidy comes with limitations, including restrictions on deployment size and CI/CD usage.

</details>

<details>

<summary>How long does deployment take?</summary>

Most deployments complete in 2-5 minutes. Factors affecting deployment time:

* Repository size
* Build complexity
* Network conditions
* Arweave network speed

</details>

<details>

<summary>What are the size limits?</summary>

* Maximum build output: 10MB
* Build timeout: 10 minutes
* For larger applications, consider:
  * Optimizing assets
  * Using lazy loading
  * Implementing code splitting

</details>

## Next Steps

Need help? Click the chat icon in the bottom right or join our [Discord community](https://discord.gg/gxGTmUyBWp).

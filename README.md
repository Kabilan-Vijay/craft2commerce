# Craft2Commerce

Craft2Commerce is a single-page marketplace prototype with a small Node.js server for secure, multilingual AI drafts.

## Run locally

Install Node.js 20 or newer, then open PowerShell in this folder and run:

```powershell
node server.mjs
```

Open <http://127.0.0.1:4173> in your browser. Marketplace, cart, saved artisan listings, and buyer matching work without an AI token.

## Enable AI drafts

Create a fine-grained Hugging Face token with **Make calls to Inference Providers** permission. Enter the token directly in PowerShell; do not paste it into the HTML, this README, or a chat:

```powershell
$secureToken = Read-Host "Hugging Face token" -AsSecureString
$env:HF_TOKEN = [System.Net.NetworkCredential]::new('', $secureToken).Password
node server.mjs
Remove-Item Env:HF_TOKEN
```

The default model is `Qwen/Qwen3-8B:fastest`. To select another model available to your Hugging Face account, set `HF_MODEL` before starting the server:

```powershell
$env:HF_MODEL = "Qwen/Qwen3-8B:fastest"
```

You may need an enabled Inference Provider and available credits. The token stays in the Node process; product fields are sent to Hugging Face only when a user requests an AI draft. Review generated text for accuracy before publishing.

The demo stores artisan-created listings in this browser's local storage. This is not a production marketplace database or payment system.
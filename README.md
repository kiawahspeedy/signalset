Signalset
Living Identity Graph (LIG) · v2.1
Identity resolution, cohort measurement, and AI-powered activation — connected through the Living Identity Graph. Built for enterprise marketing teams operating in a privacy-first, clean-room environment.

Platform Modules
ModuleDescriptionIdentity GraphDeterministic resolution across 221M nodes · 7+ devices · household graph · 94% match rateMeasurementLTV/CAC cohort analysis · 3-level micro-cohort drill · US geo intelligence · clean-room attributionActivation — In-HouseSmart Audience · Smart Triggers · Creative Selector · Destinations · Brief BuilderActivation — MerchantsAudience Discovery · Campaign Builder · Manage Campaigns · Results & Attribution

Tech Stack
LayerTechnologyFrontendReact 18 (CDN/Babel) · Satoshi + IBM Plex Mono · D3.jsAIClaude via Anthropic API (Haiku)HostingCloudflare PagesAuthCloudflare Workers · KV · Resend OTPData vizD3 force simulation · bubble charts · US geo map

Repo Structure
signaset/
├── index.html       # Full platform — splash, auth gate, all modules
├── worker.js        # Cloudflare Worker — OTP auth (deploy separately)
├── .gitignore
├── LICENSE
└── README.md

Deployment
Cloudflare Pages (frontend)

Connect this repo in the Cloudflare dashboard → Workers & Pages → Create → Pages
No build command. Build output directory: /
Every push to main triggers an automatic redeploy

Auth Worker (backend)
Deploy worker.js separately as a Cloudflare Worker with the following bindings:
KV Namespace
Binding name: AUTH_CODES
Environment Variables / Secrets
VariableDescriptionRESEND_API_KEYAPI key from resend.comFROM_EMAILSending address e.g. auth@signalset.ioHMAC_SECRETRandom secret — generate with: openssl rand -hex 32ALLOWED_EMAILSOptional comma-separated allowlist. Leave empty for open access.
Worker endpoints

POST /send-otp — sends 6-digit code to email
POST /verify-otp — validates code, returns session token
POST /verify-token — validates existing session token


Auth Flow
signalset.io (public splash)
  → click Identity / Measurement / Activation
    → passphrase gate (current) / OTP email (production)
      → platform unlocks for session

Status

 Splash page + public marketing site
 Auth gate (passphrase)
 Auth gate (OTP worker — wired to email)
 Pricing page
 Activation dropdown complete
 AI system prompt rewrite (Signalset brand voice)
 signalset.io custom domain live


Built by
Dio Favatas · Favatas Signalworks · https://signalworx.io

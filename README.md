# PentestGPT - Bug Bounty Reconnaissance

## Environnement

Lab de pentesting éthique sur Ubuntu 24.04 avec outils de reconnaissance, scan, exploitation et reporting.

## Structure

```
/workspaces/apk/
├── pentest/
│   ├── recon/           # Rapports de reconnaissance
│   │   ├── auth/        # Analyse authentification SSO
│   │   ├── js/          # Analyse bundles JavaScript
│   │   ├── takeover/    # Analyse subdomain takeover
│   │   └── *.md         # Rapports formatés
│   ├── scripts/         # Scripts helpers
│   ├── wordlists/       # SecLists et dictionnaires
│   └── README.md        # Documentation détaillée
├── tools/               # Scripts d'installation
└── README.md
```

## Cible : Vercel (Bug Bounty - HackerOne)

Reconnaissance complète de `*.vercel.com` effectuée en 10 phases.

### Findings clés

| Finding | Sévérité | Fichier |
|---|---|---|
| CORS `*` permissif sur TOUS endpoints /v1/* | Medium | `rapport-cors-deep.md` |
| /v1/certs → 500 systématique (sans auth) | Medium | `rapport-v1-certs-deep.md` |
| /api/contentful-webhook-docs-tags → 500 | Medium | `rapport-contentful-webhook-500.md` |
| 57 endpoints API découverts via JS | Info | `rapport-endpoints-caches.md` |
| 11 sous-domaines orphelins (404) | Low | `rapport-takeover-deep.md` |
| CSP `unsafe-eval` + `unsafe-inline` | Low | `rapport-recon-vercel.md` |
| Divulgation stack (X-Powered-By) | Low | `rapport-recon-vercel.md` |
| SSO Okta via WorkOS (nonce, JWT) | Info | `rapport-auth-sso-deep.md` |
| analytics.vercel.com + data.vercel.com 404 | Low | `rapport-subdomain-new.md` |

### Phases réalisées (15 au total)

- [x] Reconnaissance passive (WHOIS, DNS, SSL)
- [x] Scan réseau (nmap, fingerprinting)
- [x] Énumération sous-domaines (288 + 31 cert.sh)
- [x] Analyse API (/v1/certs, contentful-webhook)
- [x] Deep dive 500 errors (2 endpoints trouvés)
- [x] Analyse JavaScript (57 endpoints, routes, webhooks)
- [x] Analyse SSO Okta (nonce, open redirect, SAML, WorkOS)
- [x] Subdomain takeover (CNAME externes vérifiés)
- [x] CORS fuzzing (wildcard confirmé)
- [x] Rapports formatés (15 fichiers) + commit/push

## Rapports disponibles

| Rapport | Contenu |
|---|---|
| `rapport-final.md` | Synthèse générale |
| `rapport-v1-certs-deep.md` | /v1/certs 500 (Medium) |
| `rapport-contentful-webhook-500.md` | Webhook 500 (Medium) |
| `rapport-cors-deep.md` | CORS wildcard (Medium) |
| `rapport-endpoints-caches.md` | 57 endpoints cachés |
| `rapport-subdomain-new.md` | analytics/data.vercel.com |
| `rapport-auth-sso-deep.md` | SSO Okta |
| `rapport-ai-chat-fuzz.md` | Fuzzing ai-chat |

Tous dans `pentest/recon/`

## Outils installés

**Réseau :** nmap, masscan, naabu, tcpdump  
**Web :** gobuster, ffuf, dirb, httpx, whatweb, nikto, wfuzz  
**Exploitation :** sqlmap, hydra, john, hashcat, impacket, pwntools  
**OSINT :** subfinder, assetfinder, waybackurls, gau  
**Wordlists :** SecLists (Discovery, Fuzzing, Passwords)  
**Infrastructure :** Metasploit (Docker), proxychains, tor

## Utilisation

```bash
source pentest/scripts/pentest-helpers.sh
scan_network 10.10.0.0/16
full_scan 10.10.10.5
web_scan http://target.com
gobuster_dir http://target.com
```

---

*Rapports confidentiels — Bug Bounty Responsible Disclosure*

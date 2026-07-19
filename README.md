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
| CORS `*` permissif sur api.vercel.com | Medium | `rapport-api-enum.md` |
| /v1/certs → 500 systématique (sans auth) | Medium | `rapport-v1-certs-deep.md` |
| 9 sous-domaines orphelins (404) | Low | `rapport-takeover-deep.md` |
| CSP `unsafe-eval` + `unsafe-inline` | Low | `rapport-recon-vercel.md` |
| Divulgation stack (X-Powered-By) | Low | `rapport-recon-vercel.md` |
| SSO Okta via WorkOS | Info | `rapport-auth-sso-deep.md` |

### Phases réalisées

- [x] Reconnaissance passive (WHOIS, DNS, SSL)
- [x] Scan réseau (nmap, fingerprinting)
- [x] Énumération sous-domaines (288 trouvés)
- [x] Analyse API (/v1/certs, /api/ai-chat)
- [x] Analyse JavaScript (endpoints cachés)
- [x] Analyse SSO Okta (nonce, open redirect, SAML)
- [x] Subdomain takeover (CNAME externes vérifiés)
- [x] Rapports formatés + commit/push

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

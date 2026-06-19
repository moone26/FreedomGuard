# 📦 Catalogue Complet — Projets Open Source Existants

> **Date** : 19 Juin 2026  
> **Recherche exhaustive** : 30+ projets analysés sur GitHub, F-Droid, et le web

---

## 1. 🤖 Android — Bloqueurs & Wellbeing

### Tier 1 : Les Plus Robustes

#### Mindful
- **URL** : https://github.com/akaMrNagar/Mindful
- **Licence** : Open source
- **Distribution** : Play Store + GitHub
- **Features** : Focus modes, blocage apps/sites, limites screen time, **"Invincible Mode"** (restrictions impossibles à changer pendant session active), gestion notifications, mode nuit, **blocage Reels/Shorts**
- **Anti-bypass** : ⭐⭐⭐⭐ — Invincible Mode rend la désactivation très difficile
- **Privacy** : 100% offline, pas d'ads/trackers, pas de compte
- **Pertinence FreedomGuard** : HAUTE — L'Invincible Mode est un concept à intégrer

#### Déchaîner
- **URL** : https://github.com/warleysr/dechainer
- **Licence** : Open source
- **Features** : Utilise les privilèges **Device Owner** pour bloquer la pornographie, empêche la désinstallation
- **Anti-bypass** : ⭐⭐⭐⭐⭐ — Device Owner mode = quasi impossible à contourner sans factory reset
- **Setup** : Complexe (nécessite ADB pour Device Owner)
- **Pertinence FreedomGuard** : TRÈS HAUTE — Le mécanisme Device Owner est le plus robuste sur Android

#### TapBlok
- **URL** : https://github.com/flxapps/TapBlok
- **Licence** : Open source
- **Features** : Nécessite un **tag NFC physique ou QR code** pour débloquer les apps — crée une friction réelle dans le monde physique
- **Anti-bypass** : ⭐⭐⭐⭐⭐ — Nécessite un objet physique (tag NFC dans une autre pièce) pour bypass
- **Pertinence FreedomGuard** : HAUTE — Concept innovant de friction physique

#### Reef
- **URL** : https://github.com/aload0/Reef
- **Licence** : MIT
- **Distribution** : GitHub, F-Droid (IzzyOnDroid)
- **Features** : Blocage apps, limites de temps quotidiennes, routines programmées, stats détaillées, timer Pomodoro, Material You
- **Anti-bypass** : ⭐⭐⭐ — Usage Access + Display Over Other Apps
- **Pertinence FreedomGuard** : MOYENNE — Bon UI/UX à étudier

### Tier 2 : Spécialisés

#### DetoxDroid
- **URL** : https://github.com/flx-apps/DetoxDroid
- **Features** : Modes niveaux de gris automatiques, réduction notifications, blocage apps, settings protégés par mot de passe
- **Pertinence** : Concept intéressant du mode niveaux de gris

#### Farhan
- **URL** : https://github.com/farhan-app/Farhan
- **Features** : Délai avant ouverture d'apps (force "réfléchir deux fois"), bloqueur de scroll infini, niveaux de gris
- **Pertinence** : Cible les "dark patterns" manipulatifs plutôt que le simple blocage

#### Scrolless
- **URL** : https://github.com/duartebarbosadev/Scrolless
- **Features** : Bloque le doomscrolling (TikTok, Instagram Reels, YouTube Shorts) via Accessibility Services
- **Pertinence** : Blocage ciblé du contenu court-format

#### Escape Launcher
- **URL** : https://github.com/GeorgeClensy/Escape-Launcher
- **Features** : Launcher minimaliste, screen time tracking, cache les apps distrayantes, compte à rebours avant ouverture
- **Pertinence** : Approche intéressante par remplacement du launcher

#### Zenith
- **URL** : https://github.com/1372Slash/Zenith
- **Features** : Material Design 3, "pauses mindful", widgets interactifs, objectifs, "Shield Mode"
- **Pertinence** : Design moderne à étudier

#### DigiPause
- **URL** : https://github.com/PranavPurwar/digipause
- **Features** : Modes de difficulté multiples (Easy, Adventure, Hard), communauté
- **Pertinence** : Gamification intéressante

#### DigiPaws
- **Distribution** : F-Droid
- **Features** : Gestion screen time, outils digital wellbeing
- **Pertinence** : Présent sur F-Droid

### Tier 3 : Contrôle Parental (Réutilisables)

#### TimeLimit
- **URL** : https://timelimit.io / Codeberg
- **Licence** : AGPLv3
- **Distribution** : F-Droid
- **Features** : Limites par app, multi-utilisateurs, blocs programmés, système de bonus, mode local ou connecté (serveur self-hosted)
- **Anti-bypass** : ⭐⭐⭐⭐ — Device Administrator, monitoring stats
- **Pertinence** : Architecture solide à étudier

#### Child Screen Time (cst)
- **URL** : https://github.com/childscreentime/cst
- **Features** : Blocage d'écran "inéchappable", tracking temps réel, **blocage touches hardware**, blocage apps
- **Anti-bypass** : ⭐⭐⭐⭐⭐ — Blocage touches hardware + overlay inéchappable
- **Pertinence** : Techniques de blocage très agressives à étudier

---

## 2. 🍎 macOS — Bloqueurs Desktop

#### SelfControl
- **URL** : https://github.com/SelfControlApp/selfcontrol
- **Stars** : ~4,400
- **Licence** : GNU GPL
- **Features** : Blacklist sites/mail servers, blocage timer-based
- **Anti-bypass** : ⭐⭐⭐⭐⭐ — **IMPOSSIBLE à contourner** même en redémarrant, supprimant l'app, ou quoi que ce soit d'autre jusqu'à expiration du timer
- **Pertinence** : LE gold standard de la robustesse sur macOS

#### Abstand
- **Licence** : AGPL v3
- **Features** : Blocage apps et sites, mode overlay plein écran, intention-setting, sessions programmées ou manuelles
- **Privacy** : Pas de compte, pas de tracking, 100% local
- **Pertinence** : Design intéressant d'intention-setting

---

## 3. 🪟 Windows — Bloqueurs Desktop

#### FreeBlock
- **URL** : https://github.com/Mikuel210/FreeBlock
- **Plateformes** : **Cross-platform** (Windows, Linux, macOS)
- **Features** : CLI, blocage apps et sites, blocage programmé, **sessions verrouillées** (impossible de désactiver avant expiration du timer)
- **Anti-bypass** : ⭐⭐⭐⭐ — Sessions timer verrouillées
- **Limitation** : CLI uniquement (pas de GUI)
- **Pertinence** : HAUTE — Le seul vrai cross-platform open source

#### FocusGuard Pro
- **URL** : https://github.com/MustafijRatul/FocusGuardRepo
- **Features** : Bloqueur d'apps, timer Pomodoro, dashboard analytics, UI "Acrylic/Glass", Python
- **Pertinence** : UI moderne pour Windows

#### Procrastinope
- **URL** : https://github.com/danesherbs/procrastinope-public
- **Features** : Blocage sites, enforcement "incassable" via challenge de caractères aléatoires, protection auto-restart, gestion web
- **Anti-bypass** : ⭐⭐⭐⭐ — Challenge aléatoire + auto-restart
- **Pertinence** : Concept de challenge intéressant

#### Website Blocker Desktop
- **URL** : https://github.com/aymendn/website-blocker-desktop
- **Features** : Flutter, blocage sites via modification fichier hosts
- **Pertinence** : Exemple Flutter pour Windows

#### DigitalWellbeingPC
- **URL** : https://github.com/swarajdhondge/digitalwellbeingpc
- **Features** : Privacy-first, screen time tracking, "Block mode" (auto-minimise apps distrayantes), "Warn mode" (notifications)
- **Pertinence** : Concept Block/Warn mode

---

## 4. 🌐 DNS — Filtrage Réseau

#### Pi-hole
- **URL** : https://github.com/pi-hole/pi-hole
- **Stars** : ~49k+
- **Licence** : EUPL
- **Features** : DNS sinkhole, blocage réseau-wide, dashboard web, serveur DHCP, blocklists personnalisables. Peut bloquer contenu adulte via listes NSFW (ex: oisd NSFW)
- **Anti-bypass** : ⭐⭐⭐ — Contournable via VPN, changement DNS, ou DoH
- **Pertinence** : Infrastructure de référence pour DNS filtering

#### AdGuard Home
- **URL** : https://github.com/AdguardTeam/AdGuardHome
- **Stars** : ~34.7k
- **Licence** : GPL v3
- **Features** : DNS blocking, DoH/DoT/DoQ natif, filtrage per-client, **contrôle parental natif** (safe search, blocage adulte), UI web moderne, **API REST complète**
- **Anti-bypass** : ⭐⭐⭐⭐ — Meilleur que Pi-hole grâce au DNS chiffré natif
- **Pertinence** : TRÈS HAUTE — Meilleure option self-hosted pour DNS filtering

#### RethinkDNS
- **URL** : https://github.com/celzero/rethink-app
- **Stars** : ~3k+
- **Plateforme** : Android
- **Features** : DNS + Firewall + VPN combinés, 190+ blocklists, firewall par app, DoH/DoT
- **Pertinence** : HAUTE — Architecture VPN+DNS de référence pour Android

#### personalDNSfilter
- **URL** : https://github.com/IngoZenz/personaldnsfilter
- **Plateforme** : Android
- **Features** : DNS filter proxy léger, fonctionne sans root, supporte DNS chiffré
- **Pertinence** : Implémentation DNS simple à étudier

#### AdAway
- **URL** : https://github.com/AdAway/AdAway
- **Stars** : ~6k+
- **Plateforme** : Android
- **Features** : Ad blocker classique, mode VPN local en plus du mode root
- **Pertinence** : Référence historique pour le filtrage DNS Android

### Services DNS Gratuits (Non self-hosted)

| Service | DNS | Blocage adulte | Personnalisable |
|---------|-----|---------------|----------------|
| **CleanBrowsing** | Family Filter, Adult Filter | ✅ Oui | ⚠️ Limité |
| **Cloudflare for Families** | 1.1.1.3 / 1.0.0.3 | ✅ Oui | ❌ Non |
| **OpenDNS FamilyShield** | 208.67.222.123 | ✅ Oui | ❌ Non |
| **NextDNS** | Custom | ✅ Oui | ✅ Très | 

---

## 5. 🔌 Extensions Navigateur

#### uBlock Origin
- **URL** : https://github.com/gorhill/uBlock
- **Stars** : ~50k+
- **Licence** : GPL v3
- **Features** : Bloqueur de contenu puissant, listes personnalisables incluant contenu adulte
- **Limitation** : Chrome MV3 réduit les fonctionnalités

#### LeechBlock NG
- **Plateformes** : Chrome, Firefox, Edge
- **Features** : 30 sets de blocage custom, scheduling complexe, budgets temps, modes "lockdown", protection mot de passe
- **Anti-bypass** : ⭐⭐⭐ — Mot de passe mais contournable en changeant de navigateur

#### BlockNSFW
- **Plateforme** : Firefox
- **Features** : Bloque automatiquement les sites pornographiques

---

## 6. 📊 Tracking & Monitoring

#### ActivityWatch
- **URL** : https://github.com/ActivityWatch/activitywatch
- **Stars** : ~18,000
- **Licence** : MPL 2.0
- **Plateformes** : Windows, macOS, Linux, Android (early)
- **Features** : Tracking automatique apps/fenêtres, détection AFK, extensions navigateur, API REST locale, dashboard web
- **Privacy** : Tout en local
- **Pertinence** : Tracking de référence mais PAS de blocage

#### Super Productivity
- **URL** : https://github.com/johannesjo/super-productivity
- **Stars** : ~12k+
- **Licence** : MIT
- **Plateformes** : Windows, macOS, Linux, Android
- **Features** : Task manager, time tracking, Pomodoro, intégration Jira/GitHub
- **Pertinence** : Bonne architecture multi-platform

---

## 7. 🏆 Classement Anti-Bypass (Tous Projets)

| # | Projet | Plateforme | Score | Technique principale |
|---|--------|-----------|-------|---------------------|
| 1 | **SelfControl** | macOS | ⭐⭐⭐⭐⭐ | Modifications kernel, survit reboots |
| 2 | **Cold Turkey** (commercial) | Windows/macOS | ⭐⭐⭐⭐⭐ | Service OS, auto-restart, bloque uninstaller |
| 3 | **Déchaîner** | Android | ⭐⭐⭐⭐⭐ | Device Owner mode |
| 4 | **TapBlok** | Android | ⭐⭐⭐⭐⭐ | Objet physique requis (NFC/QR) |
| 5 | **Child Screen Time** | Android | ⭐⭐⭐⭐⭐ | Blocage touches hardware + overlay |
| 6 | **Pluckeye** (gratuit, closed) | Win/Mac/Lin | ⭐⭐⭐⭐⭐ | Système de délai, system-level |
| 7 | **Mindful** | Android | ⭐⭐⭐⭐ | Invincible Mode |
| 8 | **FreeBlock** | Cross-platform | ⭐⭐⭐⭐ | Sessions timer verrouillées |
| 9 | **Procrastinope** | Cross-platform | ⭐⭐⭐⭐ | Challenge caractères + auto-restart |
| 10 | **LeechBlock NG** | Navigateur | ⭐⭐⭐ | Mot de passe |

---

## 8. 🧩 Ce qu'on Peut Réutiliser

### Composants Open Source Intégrables

| Composant | Source | Licence | Usage dans FreedomGuard |
|-----------|--------|---------|------------------------|
| DNS filtering logic | RethinkDNS | Apache 2.0 | Base pour le VPN DNS filter Android |
| Blocklists | OISD, StevenBlack | Domaine public | Listes de domaines à bloquer |
| Screen Time tracking | ActivityWatch | MPL 2.0 | Inspiration pour le tracking |
| Device Owner setup | Déchaîner | Open source | Procédure de setup Device Owner |
| NFC/QR friction | TapBlok | Open source | Friction physique optionnelle |

---

*Ce catalogue est basé sur une recherche exhaustive de 30+ projets à travers GitHub, F-Droid, et le web (Juin 2026).*

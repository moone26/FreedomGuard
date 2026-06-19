# 🧩 Composants Open Source Réutilisables — Plan de Réduction du Temps de Dev

> **Objectif** : Identifier exactement quel code existant on peut prendre, fork, ou intégrer pour
> **diviser le temps de développement par 2-3x**  
> **Date** : 19 Juin 2026

---

## 💡 Stratégie Globale : NE PAS Réinventer la Roue

```
APPROCHE CLASSIQUE (tout coder) :         12-18 mois
APPROCHE SMART (réutiliser + assembler) :  5-8 mois  ← NOTRE APPROCHE
```

**Principe** : Chaque fonctionnalité critique a DÉJÀ un projet open source qui l'implémente.
Notre travail = **assembler les meilleurs composants + ajouter le protocole de guérison**.

---

## 🤖 ANDROID — Composants à Picker

### 1. VPN + DNS Filtering → **Écrire en Kotlin inspiré de personalDNSfilter + RethinkDNS**

| Critère | Détail |
|---------|--------|
| **Approche** | Écrire ~1000-2000 lignes de Kotlin en s'inspirant des patterns existants |
| **Référence #1** | [personalDNSfilter](https://github.com/IngoZenz/personaldnsfilter) — GPL v2, Java, ~10-20K lignes, LÉGER et bien structuré |
| **Référence #2** | [RethinkDNS](https://github.com/celzero/rethink-app) — Apache 2.0, Kotlin+Go, le plus complet mais trop gros |
| **Ce qu'on copie (patterns)** | VPN TUN setup, packet loop, DNS query parsing, blocklist lookup (hash/trie), réponse NXDOMAIN crafting |
| **Ce qu'on NE copie PAS** | Le code brut (trop couplé aux apps d'origine). On réécrit proprement en Kotlin |
| **Blocklists** | Format hosts standard → [OISD NSFW](https://nsfw.oisd.nl/) + [StevenBlack](https://github.com/StevenBlack/hosts) (domaine public / MIT) |
| **Pourquoi ne pas fork** | personalDNSfilter = trop couplé au service Android. RethinkDNS = overkill (Go runtime). Nos ~1-2K lignes de Kotlin feront exactement ce qu'il faut |
| **Temps** | **~2 semaines** (au lieu de 5 en partant de zéro, grâce aux patterns copiés) |
| **Alternative directe** | Importer le **firestack .aar** de RethinkDNS (Apache 2.0) comme bibliothèque si on veut aller plus vite — mais ajoute ~15MB à l'APK |

### 2. Accessibility Service + App Blocking → **Child Screen Time** (MIT) + patterns de **Mindful**

| Critère | Détail |
|---------|--------|
| **Projet principal** | [Child Screen Time (cst)](https://github.com/childscreentime/cst) |
| **Licence** | **MIT** ✅ la plus permissive |
| **Langage** | Java (compatible Kotlin) |
| **Ce qu'on prend** | Overlay plein écran "inéchappable", **Lock Task Mode** (bloque touches Home/Back/Recent), Foreground Service + WorkManager pour persistance, protection par mot de passe |
| **Pourquoi** | MIT = on peut TOUT copier. Le blocage hardware keys est le plus robuste trouvé |
| **Temps gagné** | **~4 semaines** de dev blocking |
| **Complément** | Étudier les **patterns** de [Mindful](https://github.com/akaMrNagar/Mindful) (Flutter+Kotlin, GPL-2.0) pour l'Invincible Mode : détecter quand l'utilisateur navigue vers Settings et presser Back automatiquement |
| **Autre repo clé** | [Android TestDPC (Google)](https://github.com/googlesamples/android-testdpc) — **Apache 2.0** — implémentation Device Owner OFFICIELLE de Google, référence ultime |
| **Autre repo utile** | [Dhizuku](https://github.com/iamr0s/Dhizuku) — Permet à d'AUTRES apps d'utiliser les privilèges Device Owner |
| **MDM open source** | [Headwind MDM](https://headwind-mdm.com) — **Apache 2.0** — MDM complet open source pour Android |

### 3. Device Owner / Anti-Désinstallation → Fork de **Déchaîner**

| Critère | Détail |
|---------|--------|
| **Projet** | [Déchaîner (warleysr)](https://github.com/warleysr/dechainer) |
| **Licence** | **Apache 2.0** ✅ très permissive |
| **Langage** | Kotlin/Android |
| **Ce qu'on prend** | Setup Device Owner via Shizuku, `setUninstallBlocked()`, blocage factory reset, blocage Safe Mode, blocage ADB, DNS forcing |
| **Pourquoi** | C'est EXACTEMENT ce qu'on veut pour l'anti-bypass. Apache 2.0 = on peut tout prendre |
| **Temps gagné** | **~2-3 semaines** de dev anti-bypass |
| **Bonus** | Recovery key system déjà implémenté |

### 4. Blocklists → Directement depuis **OISD / StevenBlack**

| Critère | Détail |
|---------|--------|
| **Source** | [OISD NSFW](https://nsfw.oisd.nl/) + [StevenBlack](https://github.com/StevenBlack/hosts) |
| **Licence** | Domaine public / MIT |
| **Ce qu'on prend** | Listes de domaines pré-catégorisées (porn, gambling, social media, ads) |
| **Format** | Fichier hosts standard → parsing trivial |
| **Temps gagné** | **~1 semaine** (pas besoin de constituer nos propres listes) |

### 5. NFC/QR Friction (optionnel) → De **TapBlok**

| Critère | Détail |
|---------|--------|
| **Projet** | [TapBlok (flxapps)](https://github.com/flxapps/TapBlok) |
| **Licence** | Open source |
| **Ce qu'on prend** | Logique NFC tag / QR code pour débloquer |
| **Temps gagné** | **~1 semaine** si on veut cette feature |

---

## 🍎 iOS — Composants à Picker

### 6. Screen Time API → **Foqos** (MIT) ⭐ MEILLEUR PROJET iOS

| Critère | Détail |
|---------|--------|
| **Projet principal** | [Foqos](https://github.com/awaseem/foqos) — **MIT** ✅ |
| **Langage** | Swift + SwiftUI |
| **Qualité** | Production — app publiée sur l'App Store, développement actif |
| **Ce qu'on prend** | FamilyControls auth, ManagedSettings shields, DeviceActivityMonitor, **NFC/QR unlock physique**, profiles de blocage, `denyAppRemoval`, App Groups pour cross-extension data, Live Activities (Dynamic Island) |
| **Pourquoi** | MIT = on peut TOUT copier. Couvre 80% de notre besoin iOS. Production-quality, pas un simple exemple |
| **Temps gagné** | **~4-5 semaines** |
| **Complément** | [react-native-device-activity](https://github.com/kingstinct/react-native-device-activity) (MIT) — excellent code Swift natif pour les extensions, même si on utilise pas React Native |
| **Référence simple** | [ScreenTime_Barebones](https://github.com/CoffeeNaeriRei/ScreenTime_Barebones) — squelette minimal pour démarrer |

> **Important** : Les APIs iOS Screen Time sont notoirement mal documentées par Apple. Ces repos sont des GOLDMINES car ils montrent les pièges et solutions.

---

## 🪟 WINDOWS — Composants à Picker

### 7. Anti-Bypass Windows → **Jiyuu** ⭐ MEILLEUR RÉFÉRENCE WINDOWS

| Critère | Détail |
|---------|--------|
| **Projet** | [Jiyuu](https://github.com/xinzhao2627/jiyuu) |
| **Ce qu'on prend** | Password locks, usage limits, **modes persistants "super strict"**, browser extension WebSocket, détection émulateur, prévention désinstallation, kill browser si extension déconnectée, analytics |  
| **Pourquoi** | Le PLUS complet pour les techniques anti-bypass sur Windows |
| **Temps gagné** | **~3 semaines** de recherche anti-bypass |

### 8. Windows Service / Watchdog → **SvcWatchDog** + crate `windows-service`

| Critère | Détail |
|---------|--------|
| **Projets service** | [SvcWatchDog](https://github.com/matjazt/SvcWatchDog) (C++) + [ecraft-watchdogservice](https://github.com/ecraft/ecraft-watchdogservice) (C++, MIT) |
| **Crate Rust** | [windows-service](https://crates.io/crates/windows-service) (MIT/Apache 2.0) — boilerplate service complet |
| **Ce qu'on prend** | Boilerplate complet pour créer un Windows Service en Rust : installation, désinstallation, event logging, lifecycle |
| **Temps gagné** | **~1 semaine** (plus besoin de coder le boilerplate service) |

### 9. WFP Network Filtering → **libwfp** (Mullvad) + **SmartDNS-rs**

| Critère | Détail |
|---------|--------|
| **WFP** | [libwfp](https://github.com/mullvad/libwfp) (C++, GPL-3.0) — wrapper WFP production-quality par Mullvad VPN |
| **DNS Proxy** | [SmartDNS-rs](https://github.com/mokeyish/smartdns-rs) (Rust) — DNS proxy local, **installable comme Windows Service**, DoT/DoQ/DoH |
| **Firewall** | [windows-firewall-rs](https://github.com/lhenry-dev/windows-firewall-rs) (Rust) — wrapper Firewall API natif |
| **Process** | [Process-prevent-killed](https://github.com/sg-first/Process-prevent-killed) — pattern dual-process |
| **Temps gagné** | **~4 semaines** (WFP + DNS + firewall + dual process) |

---

## 📊 RÉSUMÉ : Matrice de Réutilisation

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    CE QU'ON CODE vs CE QU'ON PREND                     │
│                                                                         │
│  ██████████░░░░░░░░░░  Android : ~60% réutilisé, ~40% codé             │
│  ████████░░░░░░░░░░░░  iOS     : ~50% réutilisé, ~50% codé             │
│  ██████░░░░░░░░░░░░░░  Windows : ~40% réutilisé, ~60% codé             │
│  ████████████████████  Core Recovery Engine : 100% codé par nous        │
│  ██████████████████░░  Blocklists : ~90% réutilisé                      │
│                                                                         │
│  TOTAL : ~50% du code sera RÉUTILISÉ de projets existants              │
└─────────────────────────────────────────────────────────────────────────┘
```

| Fonctionnalité | Source | Licence | Temps gagné |
|----------------|--------|---------|-------------|
| DNS VPN Filtering (Android) | Patterns de personalDNSfilter + RethinkDNS | GPL v2 / Apache 2.0 | **2 sem.** |
| App Blocking + Overlay | Child Screen Time (MIT) + patterns Mindful | MIT / GPL-2.0 | **4 sem.** |
| Device Owner Anti-Uninstall | Déchaîner + Android TestDPC | Apache 2.0 | **3 sem.** |
| Blocklists (porn, social, etc.) | OISD + StevenBlack | Public domain / MIT | **1 sem.** |
| NFC/QR Friction | TapBlok (Apache 2.0) | Apache 2.0 | **1 sem.** |
| iOS Screen Time complet | **Foqos** (MIT) ⭐ | MIT | **5 sem.** |
| Windows Anti-Bypass | **Jiyuu** | Open source | **3 sem.** |
| Windows Service + Watchdog | SvcWatchDog + crate windows-service | MIT | **2 sem.** |
| Windows WFP + DNS Proxy | libwfp + SmartDNS-rs | GPL-3.0 / Open | **4 sem.** |
| | | | |
| Recovery Engine 30 jours | ✅ NOUS (unique) | — | — |
| Accountability Partner P2P | ✅ NOUS (unique) | — | — |
| UI/UX (toutes plateformes) | ✅ NOUS (notre identité) | — | — |
| Cooling-Off System | ✅ NOUS (inspiré Pluckeye) | — | — |
| | | | |
| **TOTAL TEMPS GAGNÉ** | | | **~25 semaines** |

---

## 🚀 Nouvelle Timeline avec Réutilisation

```
AVANT (tout coder) :           12-18 mois
APRÈS (réutiliser + assembler) : 5-8 mois

   Mois 1-2         Mois 3-4         Mois 5-6         Mois 7-8
   ├────────────────┼────────────────┼────────────────┼──────────┤
   │                │                │                │          │
   │ ANDROID        │ ANDROID        │ iOS +          │ Polish   │
   │ Intégration    │ Beta +         │ Windows        │ + Launch │
   │ composants     │ Recovery       │                │          │
   │ + Core         │ Engine         │                │          │
   │                │                │                │          │
   ▼                ▼                ▼                ▼          │
  Fork + Assemble  Beta F-Droid    Multi-platform   v1.0  🚀   │
```

---

## 🔧 Plan d'Action Concret : Semaine 1

```
JOUR 1-2 : FORKS
├── Fork personalDNSfilter → freedomguard-dns
├── Fork Déchaîner → étudier le code Device Owner
├── Fork ScreenBreak → étudier le code iOS
├── Cloner SvcWatchDog → base Windows
└── Télécharger blocklists OISD + StevenBlack

JOUR 3-4 : ASSEMBLAGE
├── Créer le monorepo FreedomGuard
├── Intégrer le module DNS de personalDNSfilter
├── Adapter le module Accessibility de Mindful
├── Intégrer le Device Owner de Déchaîner
└── Faire tourner un premier prototype

JOUR 5 : PREMIER TEST
├── APK qui bloque un site via DNS ✅
├── APK qui bloque une app via Accessibility ✅
├── APK qui résiste à la désinstallation ✅
└── PROTOTYPE FONCTIONNEL EN 1 SEMAINE
```

---

## ⚖️ Compatibilité des Licences

| Projet | Licence | Compatible GPLv3 ? | Obligation |
|--------|---------|-------------------|------------|
| personalDNSfilter | GPL v2 | ✅ Oui (GPLv2→v3) | Garder open source |
| Déchaîner | Apache 2.0 | ✅ Oui | Attribution simple |
| Mindful | À vérifier | Probablement ✅ | Vérifier avant |
| TapBlok | Open source | ✅ Probablement | Vérifier |
| ScreenBreak | Open source | ✅ Probablement | Vérifier |
| OISD | Domaine public | ✅ Oui | Rien |
| StevenBlack | MIT | ✅ Oui | Attribution |
| SvcWatchDog | Open source | ✅ Probablement | Vérifier |
| ecraft-watchdog | MIT | ✅ Oui | Attribution |
| windows-service (Rust) | MIT/Apache 2.0 | ✅ Oui | Attribution |

---

## 🎯 Ce que NOUS codons (notre valeur ajoutée unique)

Les projets existants font du blocage. **Personne ne fait ça** :

| Notre valeur unique | Pourquoi c'est important |
|--------------------|--------------------------|
| 🧠 **Recovery Engine 30 jours** | Programme guidé quotidien basé sur Dr. Lembke — AUCUN bloqueur ne fait ça |
| 👥 **Accountability Partner P2P** | Communication chiffrée, notifications cross-platform — les alternatives open source sont mortes |
| ⏳ **Cooling-Off System** | Délai de refroidissement inspiré de Pluckeye mais en open source |
| 🎨 **UX empathique** | Pas de jugement, tolérant aux rechutes, "Dopamine Menu" |
| 🔗 **L'intégration** | Assembler TOUT ça en UN seul produit cross-platform unifié |

---

*La vraie innovation n'est pas dans le code de blocage (il existe déjà). C'est dans l'ASSEMBLAGE intelligent + le protocole de guérison.*

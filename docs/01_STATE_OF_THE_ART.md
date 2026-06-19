# 🧠 État de l'Art — Blocage d'Addiction Numérique

> **Projet** : FreedomGuard (nom de travail)  
> **Date** : 19 Juin 2026  
> **Objectif** : Créer un produit open-source, gratuit et cross-platform pour aider les personnes souffrant d'addictions numériques (réseaux sociaux, pornographie, jeux, etc.) à travers un blocage robuste et un protocole de guérison basé sur la science.

---

## 1. Fondements Scientifiques

### 1.1 Le Protocole de Dr. Anna Lembke (Stanford)

Dr. Anna Lembke, psychiatre spécialiste des addictions à Stanford et auteure de *"Dopamine Nation"*, recommande un **protocole d'abstinence de 30 jours minimum** pour restaurer les voies de récompense du cerveau.

#### Pourquoi 30 jours ?

| Phase | Durée | Ce qui se passe |
|-------|-------|-----------------|
| **Sevrage aigu** | Jours 1-7 | Irritabilité, anxiété, envies intenses. Le système de récompense réagit à la perte de stimulation. |
| **Ajustement** | Jours 8-21 | Le cerveau commence à normaliser sa réponse aux stimuli. L'ennui apparaît — c'est un signe positif. |
| **Reset** | Jours 22-30 | Clarté mentale améliorée, meilleur contrôle des impulsions, sensibilité accrue aux plaisirs simples. |
| **Restructuration profonde** | 90 jours - 1 an+ | Restructuration neuroplastique significative. Renforcement du cortex préfrontal. |

#### La métaphore de la balance plaisir-douleur
- Le cerveau maintient un équilibre entre plaisir et douleur (homéostasie)
- La surstimulation (scrolling compulsif, porno, etc.) provoque une "down-régulation" des récepteurs dopaminergiques
- Le cerveau compense en basculant vers le côté "douleur" → anxiété, dépression, irritabilité
- **Il faut environ 30 jours pour que ces processus s'inversent**
- ~80% des personnes rapportent se sentir significativement mieux après 30 jours

#### Le protocole en 4 étapes
1. **Identifier la drogue** : Déterminer le comportement/substance problématique spécifique
2. **Abstinence totale** : Éliminer complètement le déclencheur pendant 30 jours
3. **Design de l'environnement** : Créer des barrières (supprimer apps, utiliser bloqueurs). La volonté seule est insuffisante.
4. **Réévaluation** : Après 30 jours, décider de continuer l'abstinence ou réintroduire de manière contrôlée

### 1.2 Autres références scientifiques

| Expert | Contribution | Pertinence |
|--------|-------------|------------|
| **Dr. Gary Wilson** | *"Your Brain on Porn"* — Neuroplasticité et addiction à la pornographie | Processus de récupération des récepteurs dopaminergiques |
| **Dr. Andrew Huberman** | Protocoles de régulation dopaminergique, neuroplasticité | Stratégies de "dopamine menu" et habitudes saines |
| **Dr. Cameron Sepah** | Inventeur du terme "dopamine fasting" (technique CBT) | Cadre thérapeutique pour le sevrage comportemental |
| **OMS** | Classification du "Gaming Disorder" (CIM-11) | Reconnaissance officielle de l'addiction aux jeux |

### 1.3 Conclusion scientifique pour notre produit
> **Notre application DOIT garantir un blocage ininterrompu de 30 jours minimum**, avec possibilité d'extension à 90 jours pour les cas sévères. Le design de l'environnement (barrières technologiques) est au cœur du protocole — c'est exactement ce que notre produit fournit.

---

## 2. Solutions Existantes — Analyse Comparative

### 2.1 Applications Commerciales (Payantes)

| Application | Plateformes | Prix | Anti-bypass | Forces | Faiblesses |
|-------------|------------|------|-------------|--------|------------|
| **Cold Turkey** | Windows, macOS | ~$39 (lifetime) | ⭐⭐⭐⭐⭐ | Blocage OS-level, auto-restart du service, empêche désinstallation pendant un bloc actif | Pas mobile, pas gratuit |
| **Freedom** | Windows, macOS, iOS, Android, Chrome | ~$7/mois | ⭐⭐⭐ | Cross-platform, sessions synchronisées | Facile à contourner, cher |
| **Opal** | iOS uniquement | ~$10/mois | ⭐⭐⭐ | Design moderne, Apple Screen Time API | iOS uniquement, abonnement |
| **one sec** | iOS, Android | Freemium | ⭐⭐ | "Friction" avant ouverture d'apps | Ne bloque pas vraiment |
| **Covenant Eyes** | Windows, macOS, iOS, Android | ~$17/mois | ⭐⭐⭐⭐ | Accountability partner, monitoring IA | Très cher, pas open source |
| **Ever Accountable** | Multi-platform | ~$7/mois | ⭐⭐⭐⭐ | Screenshots, monitoring, ISO certifié | Payant |
| **Pluckeye** | Windows, macOS, Linux | Gratuit | ⭐⭐⭐⭐⭐ | Système de délai, très robuste, system-level | Pas mobile, UX complexe, closed-source |

### 2.2 Projets Open Source

| Projet | GitHub | Plateformes | Stars | Maintenu | Forces | Faiblesses |
|--------|--------|------------|-------|----------|--------|------------|
| **FreeBlock** | [Mikuel210/FreeBlock](https://github.com/Mikuel210/FreeBlock) | Linux, macOS, Windows | ~faible | Oui | CLI, timed locks, "pas de workaround" | CLI uniquement, pas mobile |
| **ActivityWatch** | [ActivityWatch/activitywatch](https://github.com/ActivityWatch/activitywatch) | Windows, macOS, Linux, Android | ~12k+ | Oui | Tracking temps d'écran, privacy-first | Pas de blocage actif |
| **Reef** | [aload0/Reef](https://github.com/aload0/Reef) | Android | ~modéré | Oui | App/website blocking, Material You | Android uniquement |
| **DigitalWellbeingPC** | [swarajdhondge/digitalwellbeingpc](https://github.com/swarajdhondge/digitalwellbeingpc) | Windows 10/11 | ~faible | Oui | Block mode, Warn mode | Windows uniquement, basique |
| **RethinkDNS** | [celzero/rethink-app](https://github.com/celzero/rethink-app) | Android | ~3k+ | Oui | DNS + Firewall + VPN, 190+ blocklists | Android uniquement |
| **AdAway** | [AdAway/AdAway](https://github.com/nickseveral/AdAway) | Android | ~6k+ | Oui | Local VPN DNS filter, classique | Pas de blocage d'apps |
| **personalDNSfilter** | [IngoZenz/personaldnsfilter](https://github.com/IngoZenz/personaldnsfilter) | Android | ~modéré | Oui | Léger, DNS proxy | DNS uniquement |
| **AdGuard Home** | [AdguardTeam/AdGuardHome](https://github.com/AdguardTeam/AdGuardHome) | Self-hosted | ~25k+ | Oui | Contrôle parental, API REST, per-client | Serveur nécessaire, pas un app |
| **Pi-hole** | [pi-hole/pi-hole](https://github.com/pi-hole/pi-hole) | Self-hosted | ~50k+ | Oui | DNS sinkhole, très populaire | Contrôle parental limité |
| **Net Responsibility** | - | Linux | - | **Abandonné** | Accountability partner open source | Discontinué |

### 2.3 Apps de Récupération (Streaks/Community)

| Application | Type | Gratuit | Forces |
|-------------|------|---------|--------|
| **I Am Sober** | Streak tracker + communauté | Freemium | Tracking, pledges, communauté |
| **Nomo** | Multi-clocks habits | Gratuit | Simple, accountability partners |
| **Relay** | Accountability groupes | Gratuit | Spécifique addiction porno, groupes anonymes |

---

## 3. Analyse des Lacunes (Gap Analysis)

### 3.1 Ce qui manque sur le marché

```
┌─────────────────────────────────────────────────────────────────────┐
│                     AUCUN PRODUIT N'OFFRE TOUT :                   │
│                                                                     │
│  ✅ Gratuit & Open Source                                          │
│  ✅ Cross-platform (Android + iOS + Windows + macOS + Linux)       │
│  ✅ Blocage robuste anti-contournement                             │
│  ✅ Protocole de guérison 30 jours (basé sur la science)           │
│  ✅ Accountability partner                                         │
│  ✅ Suivi de progrès (streak, stats)                               │
│  ✅ Protection contre la désinstallation                            │
│  ✅ Blocage de contenu (DNS + App)                                 │
│                                                                     │
│  → C'EST NOTRE OPPORTUNITÉ                                        │
└─────────────────────────────────────────────────────────────────────┘
```

### 3.2 Matrice des opportunités

| Besoin | Couvert par | Notre avantage |
|--------|-------------|----------------|
| Blocage d'apps cross-platform | Rien de gratuit et robuste | Première solution open source cross-platform |
| Protocole 30 jours guidé | Aucune app blocker | Intégration science + technique |
| Anti-désinstallation | Cold Turkey (payant, desktop) | Open source, mobile + desktop |
| DNS filtering + App blocking combinés | Aucun produit unifié | Solution tout-en-un |
| Accountability partner gratuit | Net Responsibility (mort) | Remplaçant moderne open source |
| Communauté & support | I Am Sober (pas blocage) | Blocage + communauté intégrés |

---

## 4. Analyse Technique des Approches Anti-Bypass

### 4.1 Android

| Technique | Robustesse | Faisabilité 2026 | Notes |
|-----------|-----------|-------------------|-------|
| **Device Administrator** (legacy) | ⭐⭐ | ⚠️ Deprecated | Google l'a sévèrement limité |
| **Android Enterprise (Device Owner)** | ⭐⭐⭐⭐⭐ | ✅ Possible | `DISALLOW_UNINSTALL_APPS`, nécessite un setup spécial |
| **Accessibility Service** | ⭐⭐⭐ | ⚠️ Restreint | Android 17+ bloque les usages non-légitimes |
| **Local VPN (VpnService)** | ⭐⭐⭐⭐ | ✅ Standard | DNS filtering, pas de root nécessaire |
| **UsageStatsManager** | ⭐⭐⭐ | ✅ Standard | Tracking usage, detection d'apps |
| **Notification Listener** | ⭐⭐ | ✅ Standard | Monitoring, pas de blocage |
| **Custom Launcher** | ⭐⭐⭐ | ✅ Possible | Restreint l'accès aux apps |
| **Work Profile** | ⭐⭐⭐⭐ | ✅ Possible | Isolation d'apps dans un profil séparé |

**Stratégie recommandée pour Android :**
- VPN local pour DNS filtering (bloquer sites)
- Device Owner/Admin pour empêcher désinstallation
- Accessibility Service (avec avertissement Google Play) pour détecter/bloquer apps
- Distribution via F-Droid + APK direct (éviter restrictions Play Store)

### 4.2 iOS

| Technique | Robustesse | Faisabilité 2026 | Notes |
|-----------|-----------|-------------------|-------|
| **Screen Time API (FamilyControls)** | ⭐⭐⭐⭐⭐ | ✅ Officiel | `denyAppRemoval = true`, blocage apps |
| **ManagedSettings Framework** | ⭐⭐⭐⭐⭐ | ✅ Officiel | Restrictions granulaires |
| **Network Extension (Content Filter)** | ⭐⭐⭐⭐ | ⚠️ Supervision requise | Filtrage réseau, nécessite MDM ou child account |
| **MDM Profile** | ⭐⭐⭐⭐⭐ | ✅ Possible | `allowDeletion = false`, contrôle total |
| **Guided Access** | ⭐⭐⭐ | ✅ Natif iOS | Mode kiosque, limité |

**Stratégie recommandée pour iOS :**
- Screen Time API avec FamilyControls → empêcher suppression de l'app
- ManagedSettings pour bloquer des apps spécifiques
- Combinaison avec un MDM léger self-hosted pour le filtrage réseau
- Soumettre à Apple avec entitlement FamilyControls (nécessite approbation Apple)

### 4.3 Windows

| Technique | Robustesse | Faisabilité 2026 | Notes |
|-----------|-----------|-------------------|-------|
| **Windows Service + Watchdog** | ⭐⭐⭐⭐ | ✅ Standard | Auto-restart, protection processus |
| **DNS Proxy local** | ⭐⭐⭐⭐ | ✅ Standard | Modification DNS système |
| **Modification hosts file** | ⭐⭐⭐ | ✅ Simple | Facile à contourner |
| **Windows Firewall API** | ⭐⭐⭐⭐ | ✅ Standard | Bloquer apps réseau |
| **Group Policy (GPO)** | ⭐⭐⭐⭐⭐ | ✅ Standard | Empêcher Add/Remove Programs |
| **ACL sur fichiers/registre** | ⭐⭐⭐⭐ | ✅ Standard | Protéger les fichiers de l'app |
| **WDAC/AppLocker** | ⭐⭐⭐⭐⭐ | ✅ Pro/Enterprise | Contrôle d'exécution |
| **WFP (Windows Filtering Platform)** | ⭐⭐⭐⭐⭐ | ✅ Avancé | Filtrage réseau kernel-level |

**Stratégie recommandée pour Windows :**
- Service Windows avec watchdog (auto-réparation)
- DNS proxy local + Windows Firewall
- Protection des fichiers par ACL
- Délai de refroidissement pour la désinstallation (comme Pluckeye)
- Browser extensions verrouillées

### 4.4 Approches Cross-Platform

| Approche | Description | Avantage |
|----------|-------------|----------|
| **DNS-over-HTTPS (DoH) personnalisé** | Serveur DNS cloud qui filtre le contenu | Fonctionne sur TOUS les appareils |
| **Configuration DNS privée** | Pointer vers un resolver filtrant | Pas d'app nécessaire |
| **Extensions navigateur** | Bloquer dans le navigateur | Cross-browser mais contournable |
| **Profil VPN/Proxy** | Tunnel tout le trafic | Très efficace mais consomme batterie |

---

## 5. Choix Technologiques Possibles

### 5.1 Framework Cross-Platform

| Technologie | Code partagé | Accès système | Performance | Écosystème |
|-------------|-------------|---------------|-------------|------------|
| **Kotlin Multiplatform (KMP)** | 60-90% | ✅ Natif | ⭐⭐⭐⭐⭐ | Mature, Google-backed |
| **Flutter** | 80-95% | ⚠️ Via Platform Channels | ⭐⭐⭐⭐ | Large communauté |
| **React Native** | 70-85% | ⚠️ Via Native Modules | ⭐⭐⭐ | Web devs friendly |
| **Natif par plateforme** | 0% | ✅ Total | ⭐⭐⭐⭐⭐ | Maximum de contrôle |

**Recommandation : Architecture hybride**
- **Core/Business Logic** : Kotlin Multiplatform (partagé entre Android, iOS, Desktop)
- **Android UI** : Jetpack Compose
- **iOS UI** : SwiftUI + Screen Time APIs
- **Windows** : Kotlin Desktop (Compose Multiplatform) + Service natif C++/Rust
- **Modules système** : Natif par plateforme (VPN, DNS, Accessibility, Services)

---

## 6. Conclusion

### Ce que nous construisons n'existe pas encore :
1. **Aucune solution gratuite et open source** ne combine blocage robuste + protocole de guérison
2. **Aucune solution cross-platform** ne couvre Android + iOS + Windows avec anti-bypass
3. **Aucune solution** n'intègre les recommandations de Dr. Lembke dans un flux guidé de 30 jours
4. **L'écosystème open source actuel est fragmenté** : des outils DNS ici, des trackers là, des bloqueurs ailleurs

### Notre produit comble TOUTES ces lacunes en un seul outil unifié.

---

*Document rédigé après analyse de 30+ sources web, projets GitHub, documentation Apple/Google, et recherche neuroscientifique.*

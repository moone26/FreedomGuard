# 🗺️ Roadmap — FreedomGuard

> **Version** : 0.1 (Draft)  
> **Date** : 19 Juin 2026  
> **Durée estimée** : 12-18 mois pour v1.0 complète

---

## Vue d'Ensemble

```
    2026                                          2027
    Q3          Q4          Q1          Q2          Q3
    ├───────────┼───────────┼───────────┼───────────┤
    │           │           │           │           │
    │ PHASE 1   │ PHASE 2   │ PHASE 3   │ PHASE 4   │
    │ Foundation│ Android   │ iOS +     │ Polish +  │
    │ + Proto   │ Beta      │ Windows   │ Community │
    │           │           │           │           │
    ▼           ▼           ▼           ▼           ▼
   Recherche   Alpha       Beta        RC          v1.0
   + Core      Android     Multi-plat  Release     Launch
```

---

## Phase 0 : Recherche & Planification (Semaines 1-3) ← NOUS SOMMES ICI

### Objectif : Tout bien penser avant de coder

| Tâche | Statut | Livrable |
|-------|--------|----------|
| État de l'art & recherche | ✅ **FAIT** | `01_STATE_OF_THE_ART.md` |
| Spécifications techniques | ✅ **FAIT** | `02_SPECIFICATIONS.md` |
| Architecture & infrastructure | ✅ **FAIT** | `03_ARCHITECTURE.md` |
| Roadmap | ✅ **FAIT** | `04_ROADMAP.md` (ce document) |
| Validation du nom "FreedomGuard" | ⬜ À faire | Recherche de marque |
| Choix de licence finale | ⬜ À faire | GPLv3 recommandé |
| Setup des repositories GitHub | ⬜ À faire | GitHub org créée |
| Identité visuelle (logo, couleurs) | ⬜ À faire | Design system |
| Recrutement premiers contributeurs | ⬜ À faire | Discord / Matrix |

---

## Phase 1 : Fondations & Prototype Android (Semaines 4-12)

### Objectif : Construire le core KMP + premier prototype Android fonctionnel

### Sprint 1-2 (Semaines 4-5) : Setup Projet

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Initialiser le monorepo KMP | 🔴 Critique | 2 jours |
| Setup Gradle multi-module | 🔴 Critique | 1 jour |
| Setup SQLDelight (schéma DB) | 🔴 Critique | 2 jours |
| Implémenter les Domain Models | 🔴 Critique | 3 jours |
| Setup CI/CD (GitHub Actions) | 🟡 Important | 2 jours |
| Setup linting (ktlint, detekt) | 🟢 Nice-to-have | 1 jour |

### Sprint 3-4 (Semaines 6-7) : Core Business Logic

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| RecoveryEngine : logique programme 30 jours | 🔴 Critique | 5 jours |
| DayContentProvider : contenu quotidien | 🔴 Critique | 3 jours |
| BlocklistManager : chargement/parsing blocklists | 🔴 Critique | 3 jours |
| CoolingOffScheduler : délai de refroidissement | 🔴 Critique | 2 jours |
| StreakTracker : compteur de streak | 🟡 Important | 1 jour |
| EncryptionManager : chiffrement journal | 🟡 Important | 2 jours |

### Sprint 5-6 (Semaines 8-9) : Android — Services Système

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| FGVpnService : VPN local pour DNS filtering | 🔴 Critique | 5 jours |
| DnsPacketParser : parsing des paquets DNS | 🔴 Critique | 3 jours |
| DnsFilter : filtrage par blocklist | 🔴 Critique | 2 jours |
| FGAccessibilityService : détection/blocage apps | 🔴 Critique | 5 jours |
| FGForegroundService : service persistant | 🔴 Critique | 2 jours |
| BootReceiver : restart au démarrage | 🟡 Important | 1 jour |

### Sprint 7-8 (Semaines 10-11) : Android — UI

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Design system (couleurs, typographie, composants) | 🔴 Critique | 3 jours |
| DashboardScreen | 🔴 Critique | 3 jours |
| SetupScreen (onboarding, config blocage) | 🔴 Critique | 4 jours |
| BlockOverlay (écran de blocage motivant) | 🔴 Critique | 2 jours |
| ProgramScreen (guide quotidien) | 🟡 Important | 3 jours |
| StatsScreen (graphiques de base) | 🟡 Important | 2 jours |

### Sprint 9 (Semaine 12) : Tests & Alpha

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Tests unitaires core KMP | 🔴 Critique | 3 jours |
| Tests instrumentés Android | 🔴 Critique | 2 jours |
| Tests anti-bypass manuels | 🔴 Critique | 2 jours |
| Build APK Alpha | 🔴 Critique | 1 jour |
| Documentation utilisateur basique | 🟡 Important | 1 jour |

### 🎯 Livrable Phase 1 : **Alpha Android**
- ✅ DNS filtering fonctionnel
- ✅ Blocage d'apps fonctionnel
- ✅ Programme 30 jours avec contenu quotidien
- ✅ Compteur de streak
- ✅ Protection basique contre la désinstallation
- ✅ UI fonctionnelle (pas encore polie)

---

## Phase 2 : Android Beta & Robustesse (Semaines 13-24)

### Objectif : Rendre l'app Android robuste + ajouter les fonctionnalités avancées

### Sprint 10-11 (Semaines 13-14) : Anti-Bypass Avancé

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Device Administrator : empêcher désinstallation | 🔴 Critique | 3 jours |
| IntegrityChecker : vérification intégrité | 🔴 Critique | 3 jours |
| TamperDetector : détection modifications | 🔴 Critique | 3 jours |
| Monitoring DNS settings | 🟡 Important | 2 jours |
| Détection VPN tiers | 🟡 Important | 1 jour |
| Vérification NTP (anti clock manipulation) | 🟢 Nice-to-have | 1 jour |

### Sprint 12-13 (Semaines 15-16) : Accountability Partner

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Génération/scan codes d'invitation | 🔴 Critique | 2 jours |
| Échange de clés E2E | 🔴 Critique | 3 jours |
| Module de notification push (Firebase FCM) | 🔴 Critique | 3 jours |
| Interface partenaire (vue minimaliste) | 🔴 Critique | 3 jours |
| Rapport hebdomadaire | 🟡 Important | 2 jours |
| Bouton SOS (contact d'urgence) | 🟡 Important | 1 jour |

### Sprint 14-15 (Semaines 17-18) : Journal & Contenu

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Journal quotidien chiffré | 🟡 Important | 3 jours |
| Check-in humeur avec slider | 🟡 Important | 1 jour |
| Exercices de respiration (animation) | 🟡 Important | 2 jours |
| "Dopamine Menu" : suggestions d'activités | 🟡 Important | 2 jours |
| Contenu éducatif (articles intégrés) | 🟡 Important | 3 jours |
| Gestion rechutes (flow empathique) | 🔴 Critique | 2 jours |

### Sprint 16-17 (Semaines 19-20) : Statistiques & Analytics

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Graphiques temps d'écran (Compose Charts) | 🟡 Important | 3 jours |
| Heatmap horaire des envies | 🟡 Important | 2 jours |
| Score de récupération | 🟡 Important | 2 jours |
| Export des données (JSON/CSV) | 🟢 Nice-to-have | 1 jour |
| Historique des streaks | 🟡 Important | 1 jour |

### Sprint 18-19 (Semaines 21-22) : Polish UI

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Animations et transitions | 🟡 Important | 3 jours |
| Dark mode complet | 🔴 Critique | 2 jours |
| Localisation FR + EN | 🔴 Critique | 3 jours |
| Accessibilité (screen reader, contraste) | 🟡 Important | 2 jours |
| Onboarding interactif | 🟡 Important | 3 jours |
| Micro-animations (streak, badges) | 🟢 Nice-to-have | 2 jours |

### Sprint 20 (Semaines 23-24) : Beta Testing

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Programme de beta testing (recrutement) | 🔴 Critique | 2 jours |
| Bug fixes de la beta | 🔴 Critique | 5 jours |
| Tests de stress anti-bypass | 🔴 Critique | 3 jours |
| Publication sur F-Droid | 🔴 Critique | 2 jours |
| Publication APK sur GitHub Releases | 🔴 Critique | 1 jour |

### 🎯 Livrable Phase 2 : **Beta Android sur F-Droid**
- ✅ Tout de la Phase 1 +
- ✅ Anti-bypass robuste multi-couches
- ✅ Accountability partner fonctionnel
- ✅ Journal & contenu éducatif
- ✅ Statistiques & graphiques
- ✅ UI polie avec animations
- ✅ FR + EN
- ✅ Disponible sur F-Droid

---

## Phase 3 : iOS + Windows (Semaines 25-40)

### Objectif : Porter FreedomGuard sur iOS et Windows

### iOS (Semaines 25-32)

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Demande entitlement FamilyControls à Apple | 🔴 Critique | 1 jour + attente |
| Setup projet Xcode + SwiftUI | 🔴 Critique | 2 jours |
| Bridge KMP ↔ Swift | 🔴 Critique | 3 jours |
| FamilyControls authorization flow | 🔴 Critique | 3 jours |
| ManagedSettings : blocage d'apps | 🔴 Critique | 5 jours |
| ShieldConfiguration : écran de blocage custom | 🔴 Critique | 3 jours |
| DeviceActivityMonitor : monitoring background | 🔴 Critique | 5 jours |
| denyAppRemoval : empêcher suppression | 🔴 Critique | 2 jours |
| UI SwiftUI (adapter depuis les specs) | 🔴 Critique | 8 jours |
| Tests + soumission App Store | 🔴 Critique | 5 jours |
| Network Extension (si entitlement approuvé) | 🟡 Important | 5 jours |

### Windows (Semaines 33-40)

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Setup projet Compose Desktop | 🔴 Critique | 2 jours |
| Windows Service principal (C++/Rust) | 🔴 Critique | 8 jours |
| DNS Proxy Service | 🔴 Critique | 5 jours |
| Process Monitor (kill apps bloquées) | 🔴 Critique | 3 jours |
| Watchdog Service | 🔴 Critique | 3 jours |
| Firewall Manager (Windows Firewall API) | 🟡 Important | 3 jours |
| Hosts file manager | 🟡 Important | 2 jours |
| IPC entre UI et Service (Named Pipes) | 🔴 Critique | 3 jours |
| ACL protection des fichiers | 🟡 Important | 2 jours |
| Installer WiX | 🔴 Critique | 3 jours |
| Browser extension (Chrome/Firefox/Edge) | 🟡 Important | 5 jours |
| UI Compose Desktop | 🔴 Critique | 5 jours |
| Tests anti-bypass Windows | 🔴 Critique | 3 jours |

### 🎯 Livrable Phase 3 : **Beta iOS + Beta Windows**
- ✅ iOS app sur TestFlight / App Store
- ✅ Windows app avec installer
- ✅ Même fonctionnalités que Android Beta
- ✅ Accountability cross-platform (Android ↔ iOS ↔ Windows)

---

## Phase 4 : Polish, Community & Launch (Semaines 41-52)

### Objectif : Préparer le lancement officiel v1.0

| Tâche | Priorité | Estimation |
|-------|----------|------------|
| Bug fixes sur les 3 plateformes | 🔴 Critique | continu |
| Tests croisés accountability partner | 🔴 Critique | 5 jours |
| Ajout langues : ES, AR | 🟡 Important | 5 jours |
| Site web du projet (landing page) | 🟡 Important | 5 jours |
| Documentation complète (user guide) | 🔴 Critique | 5 jours |
| Documentation contributeur (dev guide) | 🟡 Important | 3 jours |
| Créer Discord/Matrix community | 🟡 Important | 1 jour |
| Programme de beta ouverte | 🔴 Critique | continu |
| Partenariats associations (NoFap, etc.) | 🟢 Nice-to-have | continu |
| Video tutoriel d'installation | 🟡 Important | 2 jours |
| Security audit (si possible via communauté) | 🟡 Important | continu |
| Release v1.0 | 🔴 Critique | 1 jour |

### 🎯 Livrable Phase 4 : **FreedomGuard v1.0** 🎉
- ✅ Android (F-Droid + APK)
- ✅ iOS (App Store)
- ✅ Windows (GitHub + Winget)
- ✅ 4 langues (FR, EN, ES, AR)
- ✅ Documentation complète
- ✅ Communauté active

---

## Post-v1.0 : Vision Long Terme

### v1.1 — Améliorations (Q3 2027)
- [ ] macOS support
- [ ] Linux support
- [ ] Thèmes personnalisés
- [ ] Programme 90 jours
- [ ] Widget Android/iOS
- [ ] Notifications intelligentes (ML basique)

### v1.2 — Communauté (Q4 2027)
- [ ] Forums de support intégrés
- [ ] Système de badges/achievements
- [ ] Témoignages anonymes partagés
- [ ] Groupes de recovery (anonymes)
- [ ] Multi-profils (famille)

### v2.0 — Innovation (2028)
- [ ] IA locale pour détection de contenu (on-device ML)
- [ ] Intégration wearables (Android Watch, Apple Watch)
- [ ] Mode "Digital Sabbath" (1 jour/semaine sans écran)
- [ ] Partenariats cliniques (thérapeutes)
- [ ] API pour intégration avec d'autres outils
- [ ] Router-level blocking (companion hardware)

---

## Ressources Nécessaires

### Équipe Minimale (Open Source)

| Rôle | Nombre | Compétences |
|------|--------|-------------|
| Lead Developer (KMP) | 1 | Kotlin, KMP, architecture |
| Android Developer | 1-2 | Kotlin, Android SDK, VpnService, Accessibility |
| iOS Developer | 1 | Swift, SwiftUI, Screen Time API |
| Windows Developer | 1 | C++/Rust, Windows Services, WFP |
| UI/UX Designer | 1 | Mobile + Desktop design, empathic design |
| Content Writer | 1 | Psychologie, addiction, contenu quotidien |
| Community Manager | 1 | Relations communauté, modération |

### Infrastructure (coûts minimaux)

| Service | Coût | Nécessité |
|---------|------|-----------|
| GitHub (free tier) | $0 | Hébergement code |
| GitHub Actions (free tier) | $0 | CI/CD |
| Apple Developer Program | $99/an | Publication iOS |
| Firebase (free tier) | $0 | Push notifications |
| Domaine freedomguard.org | ~$12/an | Site web |
| Code signing certificate (Windows) | ~$100/an | Signer l'installeur |
| **Total annuel** | **~$211/an** | |

---

## Indicateurs de Succès

| Métrique | Cible 6 mois | Cible 1 an |
|----------|-------------|-----------|
| Téléchargements totaux | 5,000 | 50,000 |
| Utilisateurs actifs mensuels | 1,000 | 10,000 |
| Stars GitHub | 500 | 5,000 |
| Contributeurs | 10 | 30 |
| Taux de complétion 30 jours | 20% | 30% |
| Note moyenne (stores) | 4.0/5 | 4.5/5 |
| Langues supportées | 2 (FR, EN) | 6 |

---

*Ce roadmap est un guide vivant. Il sera ajusté en fonction des retours de la communauté, des contraintes techniques découvertes en cours de route, et des priorités émergentes.*

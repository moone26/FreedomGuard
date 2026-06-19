# 🏗️ Architecture & Infrastructure — FreedomGuard

> **Version** : 0.1 (Draft)  
> **Date** : 19 Juin 2026

---

## 1. Vision Architecturale

### 1.1 Contraintes Fondamentales

Notre app doit résoudre un **paradoxe unique** : une app que l'utilisateur installe volontairement mais qui doit résister à ses propres tentatives de suppression. C'est radicalement différent d'une app normale.

```
                    ┌──────────────────────────────┐
                    │    L'UTILISATEUR RATIONNEL    │
                    │   installe FreedomGuard et    │
                    │   configure le blocage        │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │    L'UTILISATEUR EN CRISE     │
                    │   essaie de contourner,       │
                    │   désinstaller, forcer l'arrêt│
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │      FREEDOMGUARD DOIT       │
                    │   RÉSISTER À L'UTILISATEUR   │
                    │   CONTRE LUI-MÊME            │
                    └──────────────────────────────┘
```

### 1.2 Principes Architecturaux

| # | Principe | Description |
|---|----------|-------------|
| 1 | **Defense in Depth** | Plusieurs couches de protection indépendantes |
| 2 | **Self-Healing** | L'app se répare automatiquement si altérée |
| 3 | **Fail-Secure** | En cas de doute, bloquer plutôt qu'autoriser |
| 4 | **Privacy by Design** | Tout en local, chiffré, minimal |
| 5 | **Platform-Native** | Utiliser les APIs officielles de chaque OS |
| 6 | **Accountability First** | Un partenaire externe est la meilleure protection |
| 7 | **Honest Limitations** | Transparence sur ce qui peut et ne peut pas être bloqué |

---

## 2. Architecture Globale

### 2.1 Vue de Haut Niveau

```
┌──────────────────────────────────────────────────────────────────────────┐
│                         FREEDOMGUARD ECOSYSTEM                          │
│                                                                          │
│  ┌─────────────────────────────────────────────────────────────────┐     │
│  │                    SHARED CORE (Kotlin Multiplatform)           │     │
│  │                                                                 │     │
│  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐            │     │
│  │  │   Domain     │ │  Recovery    │ │  Blocklist   │            │     │
│  │  │   Models     │ │  Protocol    │ │  Manager     │            │     │
│  │  └──────────────┘ └──────────────┘ └──────────────┘            │     │
│  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐            │     │
│  │  │   Stats      │ │  Crypto      │ │  Scheduler   │            │     │
│  │  │   Engine     │ │  Utils       │ │  Engine      │            │     │
│  │  └──────────────┘ └──────────────┘ └──────────────┘            │     │
│  │  ┌──────────────┐ ┌──────────────┐                              │     │
│  │  │  Database    │ │  Config      │                              │     │
│  │  │  (SQLDelight)│ │  Manager     │                              │     │
│  │  └──────────────┘ └──────────────┘                              │     │
│  └─────────────────────────────────────────────────────────────────┘     │
│                              │                                           │
│         ┌────────────────────┼────────────────────┐                      │
│         ▼                    ▼                    ▼                      │
│  ┌─────────────┐    ┌──────────────┐    ┌────────────────┐              │
│  │   ANDROID   │    │     iOS      │    │    WINDOWS     │              │
│  │   Module    │    │    Module    │    │    Module      │              │
│  │             │    │             │    │                │              │
│  │ ┌─────────┐│    │ ┌─────────┐ │    │ ┌────────────┐ │              │
│  │ │VPN      ││    │ │Screen   │ │    │ │Win Service │ │              │
│  │ │Service  ││    │ │Time API │ │    │ │(SYSTEM)    │ │              │
│  │ ├─────────┤│    │ ├─────────┤ │    │ ├────────────┤ │              │
│  │ │Access.  ││    │ │Family   │ │    │ │Watchdog    │ │              │
│  │ │Service  ││    │ │Controls │ │    │ │Service     │ │              │
│  │ ├─────────┤│    │ ├─────────┤ │    │ ├────────────┤ │              │
│  │ │Device   ││    │ │Managed  │ │    │ │DNS Proxy   │ │              │
│  │ │Admin    ││    │ │Settings │ │    │ │Service     │ │              │
│  │ ├─────────┤│    │ ├─────────┤ │    │ ├────────────┤ │              │
│  │ │Foreground│    │ │Device   │ │    │ │Firewall    │ │              │
│  │ │Service  ││    │ │Activity │ │    │ │Manager     │ │              │
│  │ ├─────────┤│    │ ├─────────┤ │    │ ├────────────┤ │              │
│  │ │Boot     ││    │ │Network  │ │    │ │Browser     │ │              │
│  │ │Receiver ││    │ │Extension│ │    │ │Extension   │ │              │
│  │ └─────────┘│    │ └─────────┘ │    │ └────────────┘ │              │
│  │             │    │             │    │                │              │
│  │ Jetpack     │    │  SwiftUI    │    │ Compose        │              │
│  │ Compose     │    │             │    │ Desktop        │              │
│  └─────────────┘    └──────────────┘    └────────────────┘              │
│                                                                          │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │                 OPTIONAL COMPONENTS                              │    │
│  │  ┌──────────────┐ ┌──────────────┐ ┌──────────────────────────┐ │    │
│  │  │ DNS Server   │ │ MDM Server   │ │ Browser Extensions       │ │    │
│  │  │ (Self-hosted)│ │ (MicroMDM)   │ │ (Chrome, Firefox, Edge)  │ │    │
│  │  │ AdGuard Home │ │ (for iOS)    │ │                          │ │    │
│  │  └──────────────┘ └──────────────┘ └──────────────────────────┘ │    │
│  └──────────────────────────────────────────────────────────────────┘    │
└──────────────────────────────────────────────────────────────────────────┘
```

### 2.2 Diagramme de Composants — Shared Core

```
shared/
├── commonMain/
│   ├── domain/
│   │   ├── models/
│   │   │   ├── AddictionType.kt          # Enum: Social, Porn, Gaming, etc.
│   │   │   ├── BlockingLevel.kt          # Enum: Soft, Medium, Hard
│   │   │   ├── RecoveryProgram.kt        # Programme 30 jours
│   │   │   ├── DayContent.kt            # Contenu quotidien (exercices, articles)
│   │   │   ├── Streak.kt                # Compteur de jours
│   │   │   ├── MoodEntry.kt             # Check-in humeur
│   │   │   ├── JournalEntry.kt          # Entrée de journal
│   │   │   ├── BlockedApp.kt            # App bloquée
│   │   │   ├── BlockedDomain.kt         # Domaine bloqué
│   │   │   ├── AccountabilityPartner.kt  # Partenaire
│   │   │   └── UserProfile.kt           # Profil local
│   │   │
│   │   ├── usecases/
│   │   │   ├── StartProgramUseCase.kt
│   │   │   ├── CheckInUseCase.kt
│   │   │   ├── GetDayContentUseCase.kt
│   │   │   ├── ManageBlocklistUseCase.kt
│   │   │   ├── CoolingOffUseCase.kt      # Délai de refroidissement
│   │   │   ├── RecordRelapseUseCase.kt
│   │   │   ├── NotifyPartnerUseCase.kt
│   │   │   └── GetStatsUseCase.kt
│   │   │
│   │   └── repositories/
│   │       ├── ProgramRepository.kt       # Interface
│   │       ├── BlocklistRepository.kt     # Interface
│   │       ├── StatsRepository.kt         # Interface
│   │       └── PartnerRepository.kt       # Interface
│   │
│   ├── data/
│   │   ├── database/
│   │   │   ├── FreedomGuardDatabase.sq    # SQLDelight schema
│   │   │   └── DatabaseDriverFactory.kt   # Expect/actual
│   │   ├── blocklists/
│   │   │   ├── BlocklistParser.kt
│   │   │   ├── BlocklistUpdater.kt
│   │   │   └── DefaultBlocklists.kt       # Embedded defaults
│   │   └── impl/
│   │       ├── ProgramRepositoryImpl.kt
│   │       ├── BlocklistRepositoryImpl.kt
│   │       ├── StatsRepositoryImpl.kt
│   │       └── PartnerRepositoryImpl.kt
│   │
│   ├── recovery/
│   │   ├── RecoveryEngine.kt              # Orchestrateur du programme
│   │   ├── DayContentProvider.kt          # Fournit le contenu quotidien
│   │   ├── MilestoneTracker.kt            # Tracking des jalons
│   │   └── content/
│   │       ├── Week1Content.kt            # Sevrage
│   │       ├── Week2Content.kt            # Ajustement
│   │       ├── Week3Content.kt            # Transformation
│   │       └── Week4Content.kt            # Reset
│   │
│   ├── crypto/
│   │   ├── EncryptionManager.kt           # AES-256-GCM
│   │   └── KeyManager.kt                 # Gestion des clés
│   │
│   ├── scheduler/
│   │   ├── CoolingOffScheduler.kt         # Gestion des délais
│   │   └── NotificationScheduler.kt      # Planification notifications
│   │
│   └── config/
│       ├── AppConfig.kt                   # Configuration globale
│       └── BlocklistConfig.kt            # Config des blocklists
│
├── androidMain/           # Implémentations Android
├── iosMain/               # Implémentations iOS
└── desktopMain/           # Implémentations Windows/Desktop
```

---

## 3. Architecture par Plateforme

### 3.1 Android — Architecture Détaillée

```
android/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml
│   │   ├── java/com/freedomguard/
│   │   │   ├── ui/                        # Jetpack Compose UI
│   │   │   │   ├── theme/
│   │   │   │   ├── screens/
│   │   │   │   │   ├── DashboardScreen.kt
│   │   │   │   │   ├── ProgramScreen.kt
│   │   │   │   │   ├── BlockingScreen.kt
│   │   │   │   │   ├── PartnerScreen.kt
│   │   │   │   │   ├── StatsScreen.kt
│   │   │   │   │   └── SetupScreen.kt
│   │   │   │   └── components/
│   │   │   │       ├── StreakCounter.kt
│   │   │   │       ├── BlockOverlay.kt     # Overlay quand app bloquée
│   │   │   │       └── BreathingExercise.kt
│   │   │   │
│   │   │   ├── services/
│   │   │   │   ├── FGVpnService.kt         # VPN local pour DNS filtering
│   │   │   │   ├── FGAccessibilityService.kt # Détection/blocage d'apps
│   │   │   │   ├── FGForegroundService.kt   # Service persistant
│   │   │   │   └── FGDeviceAdminReceiver.kt  # Device Administrator
│   │   │   │
│   │   │   ├── receivers/
│   │   │   │   ├── BootReceiver.kt          # Restart au démarrage
│   │   │   │   ├── PackageReceiver.kt       # Détection install/uninstall
│   │   │   │   └── AlarmReceiver.kt         # Vérification périodique
│   │   │   │
│   │   │   ├── dns/
│   │   │   │   ├── DnsResolver.kt           # Résolution DNS
│   │   │   │   ├── DnsFilter.kt             # Filtrage par blocklist
│   │   │   │   ├── DnsPacketParser.kt       # Parsing paquets DNS
│   │   │   │   └── DnsCache.kt              # Cache DNS local
│   │   │   │
│   │   │   ├── monitoring/
│   │   │   │   ├── AppUsageMonitor.kt       # UsageStatsManager
│   │   │   │   ├── IntegrityChecker.kt      # Vérification intégrité
│   │   │   │   └── TamperDetector.kt        # Détection modifications
│   │   │   │
│   │   │   └── di/                          # Dependency Injection
│   │   │       └── AppModule.kt
│   │   │
│   │   └── res/
│   │       ├── xml/
│   │       │   ├── device_admin.xml
│   │       │   └── accessibility_service_config.xml
│   │       └── ...
```

#### Flux de Blocage Android

```
┌─────────────────────────────────────────────────────────────────┐
│                    FLUX DE BLOCAGE ANDROID                       │
│                                                                 │
│  L'utilisateur ouvre Instagram (bloqué)                         │
│           │                                                     │
│           ▼                                                     │
│  ┌──────────────────────────────────┐                           │
│  │  AccessibilityService détecte    │                           │
│  │  TYPE_WINDOW_STATE_CHANGED       │                           │
│  │  Package: com.instagram.android  │                           │
│  └──────────────┬───────────────────┘                           │
│                 │                                                │
│                 ▼                                                │
│  ┌──────────────────────────────────┐                           │
│  │  Vérification dans la blocklist  │                           │
│  │  → Instagram est dans la liste   │                           │
│  └──────────────┬───────────────────┘                           │
│                 │                                                │
│           ┌─────┴─────┐                                         │
│           │           │                                         │
│     SOFT MODE    HARD MODE                                      │
│           │           │                                         │
│           ▼           ▼                                         │
│  ┌────────────┐ ┌──────────────┐                                │
│  │ Affiche    │ │ Perform      │                                │
│  │ overlay    │ │ GLOBAL_      │                                │
│  │ motivant + │ │ ACTION_BACK  │                                │
│  │ compteur   │ │ + overlay    │                                │
│  │ respiration│ │ plein écran  │                                │
│  └────────────┘ └──────────────┘                                │
│                         │                                       │
│                         ▼                                       │
│            ┌──────────────────────┐                              │
│            │ Log de la tentative  │                              │
│            │ + notification       │                              │
│            │ accountability       │                              │
│            │ partner (si activé)  │                              │
│            └──────────────────────┘                              │
└─────────────────────────────────────────────────────────────────┘
```

#### Flux DNS Filtering Android

```
┌─────────────────────────────────────────────────────────────────┐
│                    FLUX DNS FILTERING                            │
│                                                                 │
│  App fait requête DNS : pornhub.com                             │
│           │                                                     │
│           ▼                                                     │
│  ┌──────────────────────────────────┐                           │
│  │  VpnService intercepte le       │                           │
│  │  paquet DNS via TUN interface    │                           │
│  └──────────────┬───────────────────┘                           │
│                 │                                                │
│                 ▼                                                │
│  ┌──────────────────────────────────┐                           │
│  │  DnsPacketParser extrait le      │                           │
│  │  nom de domaine                  │                           │
│  └──────────────┬───────────────────┘                           │
│                 │                                                │
│                 ▼                                                │
│  ┌──────────────────────────────────┐                           │
│  │  DnsFilter vérifie contre les    │                           │
│  │  blocklists chargées en mémoire  │                           │
│  └──────────┬───────────┬───────────┘                           │
│             │           │                                       │
│        BLOQUÉ       NON BLOQUÉ                                  │
│             │           │                                       │
│             ▼           ▼                                       │
│  ┌──────────────┐ ┌──────────────┐                              │
│  │ Retourne     │ │ Forward vers │                              │
│  │ 0.0.0.0      │ │ upstream DNS │                              │
│  │ (NXDOMAIN)   │ │ (DoH/DoT)   │                              │
│  └──────────────┘ └──────────────┘                              │
└─────────────────────────────────────────────────────────────────┘
```

### 3.2 iOS — Architecture Détaillée

```
ios/
├── FreedomGuard/
│   ├── App/
│   │   ├── FreedomGuardApp.swift
│   │   └── AppDelegate.swift
│   │
│   ├── Views/                              # SwiftUI
│   │   ├── DashboardView.swift
│   │   ├── ProgramView.swift
│   │   ├── BlockingView.swift
│   │   ├── PartnerView.swift
│   │   ├── StatsView.swift
│   │   ├── SetupView.swift
│   │   └── Components/
│   │       ├── StreakCounterView.swift
│   │       ├── BreathingView.swift
│   │       └── ProgressRingView.swift
│   │
│   ├── ScreenTime/                         # Screen Time API
│   │   ├── FGFamilyControlsManager.swift   # Authorization
│   │   ├── FGManagedSettingsManager.swift   # App blocking
│   │   ├── FGShieldConfiguration.swift     # Custom block screen
│   │   └── FGScheduleManager.swift          # Scheduling
│   │
│   ├── Extensions/                         # App Extensions
│   │   ├── DeviceActivityMonitor/          # Background monitoring
│   │   │   └── FGDeviceActivityMonitor.swift
│   │   ├── ShieldConfiguration/            # Custom shield UI
│   │   │   └── FGShieldConfigurationExtension.swift
│   │   └── ShieldAction/                   # Shield button actions
│   │       └── FGShieldActionExtension.swift
│   │
│   ├── Networking/
│   │   └── ContentFilterProvider.swift      # Network Extension (if approved)
│   │
│   └── KMPBridge/
│       └── SharedBridge.swift              # Bridge vers le core KMP
│
├── FreedomGuard.entitlements
└── Info.plist
```

#### Flux de Blocage iOS

```
┌─────────────────────────────────────────────────────────────────┐
│                    FLUX DE BLOCAGE iOS                           │
│                                                                 │
│  L'utilisateur tape sur Instagram (bloqué)                      │
│           │                                                     │
│           ▼                                                     │
│  ┌──────────────────────────────────┐                           │
│  │  iOS détecte que l'app a un      │                           │
│  │  Shield via ManagedSettings      │                           │
│  └──────────────┬───────────────────┘                           │
│                 │                                                │
│                 ▼                                                │
│  ┌──────────────────────────────────┐                           │
│  │  ShieldConfigurationExtension    │                           │
│  │  fournit l'écran de blocage      │                           │
│  │  personnalisé :                  │                           │
│  │  - Message de motivation         │                           │
│  │  - Streak actuel                 │                           │
│  │  - Bouton "Respirer"            │                           │
│  └──────────────┬───────────────────┘                           │
│                 │                                                │
│                 ▼                                                │
│  ┌──────────────────────────────────┐                           │
│  │  ShieldActionExtension gère      │                           │
│  │  les boutons de l'écran :        │                           │
│  │  - "OK, je résiste" → ferme      │                           │
│  │  - "Exercice de respiration"     │                           │
│  │    → mini exercice 1 min         │                           │
│  └──────────────────────────────────┘                           │
│                                                                 │
│  EN PARALLÈLE :                                                 │
│  ┌──────────────────────────────────┐                           │
│  │  DeviceActivityMonitor           │                           │
│  │  (fonctionne même si app fermée) │                           │
│  │  → Track usage en background     │                           │
│  │  → Réapplique shields si enlevés │                           │
│  │  → Notifie accountability partner│                           │
│  └──────────────────────────────────┘                           │
└─────────────────────────────────────────────────────────────────┘
```

### 3.3 Windows — Architecture Détaillée

```
windows/
├── FreedomGuardApp/                       # UI Application
│   ├── src/
│   │   ├── main/kotlin/com/freedomguard/
│   │   │   ├── Main.kt                    # Entry point Compose Desktop
│   │   │   ├── ui/
│   │   │   │   ├── screens/               # Same as Android (shared via KMP)
│   │   │   │   └── theme/
│   │   │   └── bridge/
│   │   │       └── ServiceBridge.kt       # Communication avec le service
│   │   └── resources/
│
├── FreedomGuardService/                   # Windows Service (C++/Rust)
│   ├── src/
│   │   ├── main.cpp (ou main.rs)
│   │   ├── service_controller.cpp         # Gestion du service Windows
│   │   ├── dns_proxy.cpp                  # Proxy DNS local
│   │   ├── process_monitor.cpp            # Surveillance des processus
│   │   ├── firewall_manager.cpp           # Windows Firewall API
│   │   ├── integrity_checker.cpp          # Vérification fichiers
│   │   ├── hosts_manager.cpp              # Gestion fichier hosts
│   │   └── ipc_server.cpp                 # Communication avec l'app UI
│   │
│   └── config/
│       └── blocklists/                    # Blocklists embarquées
│
├── FreedomGuardWatchdog/                  # Watchdog Service
│   ├── src/
│   │   ├── main.cpp
│   │   ├── watchdog.cpp                   # Surveille le service principal
│   │   └── self_repair.cpp                # Auto-réparation
│
├── FreedomGuardBrowserExt/                # Extension navigateur
│   ├── manifest.json
│   ├── background.js
│   ├── content.js
│   └── blocked.html
│
└── installer/
    ├── FreedomGuardInstaller.wxs          # WiX installer
    └── setup_script.ps1                   # Script de configuration
```

#### Architecture Services Windows

```
┌─────────────────────────────────────────────────────────────────┐
│                ARCHITECTURE SERVICES WINDOWS                     │
│                                                                 │
│  ┌─────────────────────┐    ┌─────────────────────┐             │
│  │  FreedomGuard UI    │    │  System Tray Icon   │             │
│  │  (Compose Desktop)  │◄──►│  (Notification)     │             │
│  └──────────┬──────────┘    └─────────────────────┘             │
│             │ IPC (Named Pipes)                                  │
│             ▼                                                    │
│  ┌──────────────────────────────────────────────────┐            │
│  │        FreedomGuard Service (NT SYSTEM)          │            │
│  │                                                  │            │
│  │  ┌────────────┐ ┌────────────┐ ┌──────────────┐ │            │
│  │  │ DNS Proxy  │ │ Process    │ │ Firewall     │ │            │
│  │  │ (port 53)  │ │ Monitor    │ │ Manager      │ │            │
│  │  └────────────┘ └────────────┘ └──────────────┘ │            │
│  │  ┌────────────┐ ┌────────────┐ ┌──────────────┐ │            │
│  │  │ Hosts File │ │ Integrity  │ │ Config       │ │            │
│  │  │ Manager    │ │ Checker    │ │ Manager      │ │            │
│  │  └────────────┘ └────────────┘ └──────────────┘ │            │
│  └──────────────────────┬───────────────────────────┘            │
│                         │ Mutual monitoring                      │
│                         ▼                                        │
│  ┌──────────────────────────────────────────────────┐            │
│  │        FreedomGuard Watchdog (NT SYSTEM)         │            │
│  │                                                  │            │
│  │  • Vérifie que le service principal tourne        │            │
│  │  • Restart si arrêté                              │            │
│  │  • Vérifie l'intégrité des fichiers               │            │
│  │  • Restaure la config si modifiée                 │            │
│  │  • Le service principal surveille aussi le watchdog│           │
│  └──────────────────────────────────────────────────┘            │
│                                                                  │
│  ┌──────────────────────────────────────────────────┐            │
│  │        Browser Extension (Chrome/Firefox/Edge)   │            │
│  │                                                  │            │
│  │  • Blocage in-browser comme couche supplémentaire │            │
│  │  • Managed par Group Policy (Chrome Enterprise)   │            │
│  │  • Communication avec le service via native msg   │            │
│  └──────────────────────────────────────────────────┘            │
└──────────────────────────────────────────────────────────────────┘
```

---

## 4. Système de Blocklists

### 4.1 Sources de Blocklists

| Source | Type | Taille | Usage |
|--------|------|--------|-------|
| **OISD NSFW** | Domains porno/adulte | ~500K domaines | Blocage pornographie |
| **StevenBlack** | Ads + tracking + porn + gambling | ~200K domaines | Multi-catégorie |
| **Energized** | Ads + tracking + malware | ~1M+ domaines | Protection large |
| **Custom user** | Défini par l'utilisateur | Variable | Personnalisation |
| **App package names** | Applications (Android) | Variable | Blocage d'apps mobiles |
| **App executables** | Exécutables (Windows) | Variable | Blocage d'apps desktop |

### 4.2 Gestion des Blocklists

```
┌──────────────────────────────────────────────────────┐
│               BLOCKLIST MANAGEMENT                    │
│                                                      │
│  Embedded (dans l'APK/app) :                         │
│  └── Blocklists par défaut (catégorisées)            │
│      ├── social_media.txt                            │
│      ├── porn_domains.txt                            │
│      ├── gambling_domains.txt                        │
│      ├── gaming_platforms.txt                        │
│      └── streaming_platforms.txt                     │
│                                                      │
│  Updates (optionnel, privacy-respecting) :           │
│  └── Téléchargement de blocklists mises à jour       │
│      ├── HTTPS direct depuis GitHub raw              │
│      ├── Vérification d'intégrité (hash SHA-256)     │
│      └── Pas de tracking de l'utilisateur             │
│                                                      │
│  User custom :                                       │
│  └── L'utilisateur peut ajouter/supprimer            │
│      ├── Domaines individuels                        │
│      ├── Apps individuelles                          │
│      └── Regex patterns                              │
│                                                      │
│  Storage optimisé :                                  │
│  └── Bloom Filter en mémoire pour lookup O(1)        │
│      ├── Trie structure pour wildcard matching        │
│      └── Cache LRU pour les requêtes fréquentes      │
└──────────────────────────────────────────────────────┘
```

---

## 5. Communication Accountability Partner

### 5.1 Architecture P2P

```
┌─────────────┐                           ┌─────────────┐
│  Utilisateur │                           │  Partenaire │
│  FreedomGuard│                           │  FreedomGuard│
│             │                           │             │
│  ┌─────────┐│     ┌───────────────┐     │┌─────────┐ │
│  │ P2P     ││     │ Relay Server  │     ││ P2P     │ │
│  │ Module  ││◄───►│ (Firebase FCM │◄───►││ Module  │ │
│  │         ││     │  / APNs       │     ││         │ │
│  │ E2E     ││     │  push only)   │     ││ E2E     │ │
│  │ Encrypted││    └───────────────┘     ││ Encrypted│ │
│  └─────────┘│                           │└─────────┘ │
└─────────────┘                           └─────────────┘

Données échangées (minimum) :
• Tentative de contournement détectée (booléen)
• Streak actuel (nombre de jours)
• Check-in quotidien (humeur 1-5)
• Demande d'aide urgente (signal)

NON échangé :
• Apps/sites spécifiques visités
• Détails des tentatives
• Journal personnel
• Données d'usage détaillées
```

### 5.2 Setup du Partenariat

```
1. Utilisateur génère un CODE D'INVITATION (6 caractères + QR code)
2. Partenaire installe FreedomGuard
3. Partenaire entre le code → lien établi
4. Échange de clés publiques (E2E)
5. Partenaire peut voir : streak, tentatives (compteur), humeur
6. Partenaire reçoit : alertes contournement, demandes d'aide
```

---

## 6. Sécurité & Intégrité

### 6.1 Modèle de Menaces

| Menace | Probabilité | Impact | Mitigation |
|--------|------------|--------|------------|
| Utilisateur désinstalle l'app | **Très haute** | Critique | Device Admin (Android), denyAppRemoval (iOS), Watchdog (Windows) |
| Utilisateur force-stop le service | **Haute** | Critique | Auto-restart, Foreground Service, Watchdog |
| Utilisateur change les DNS | **Haute** | Élevé | Monitoring DNS settings, VPN force |
| Utilisateur boot en Safe Mode | **Moyenne** | Critique | Device Owner (Android), Service persistence (Windows) |
| Utilisateur utilise un autre navigateur | **Haute** | Moyen | DNS-level blocking (affecte tous les navigateurs) |
| Utilisateur change l'horloge système | **Moyenne** | Élevé | NTP verification, monotonic clock |
| Utilisateur root/jailbreak le device | **Basse** | Critique | Détection root/jailbreak, avertissement |
| Utilisateur connecte un VPN tiers | **Moyenne** | Élevé | Détection VPN actif, avertissement |

### 6.2 Principe de Transparence

> **FreedomGuard est HONNÊTE avec l'utilisateur.** Nous ne cachons pas ce que nous faisons. Nous expliquons chaque couche de protection et pourquoi elle existe. Si un utilisateur VEUT vraiment contourner, il trouvera un moyen — mais notre rôle est de rendre ça suffisamment difficile pour que l'envie passe.

---

## 7. Considérations Éthiques

### 7.1 Ce que FreedomGuard N'EST PAS

| Ce que nous ne sommes PAS | Pourquoi |
|--------------------------|---------|
| **Pas un spyware** | Aucune donnée envoyée à des serveurs |
| **Pas un rootkit** | Utilisation d'APIs officielles uniquement |
| **Pas un outil de contrôle parental** | Conçu pour l'AUTO-contrôle d'adultes |
| **Pas un remplacement de thérapie** | Complément technologique, pas substitut médical |
| **Pas un outil de surveillance** | Le partenaire ne voit que le minimum |

### 7.2 Désinstallation Éthique

FreedomGuard peut TOUJOURS être désinstallé, mais avec des **freins intentionnels** :
1. **Délai de refroidissement** (24h-7j configurable)
2. **Notification au partenaire** (si configuré)
3. **Confirmation multiple** ("Es-tu sûr ? Tu es à [X] jours de streak")
4. **Procédure documentée** (toujours disponible dans l'aide)

---

## 8. Infrastructure de Développement

### 8.1 Repositories

```
github.com/freedomguard/
├── freedomguard-core           # Shared KMP core
├── freedomguard-android        # Android app
├── freedomguard-ios            # iOS app
├── freedomguard-windows        # Windows app + services
├── freedomguard-browser-ext    # Browser extensions
├── freedomguard-blocklists     # Maintained blocklists
├── freedomguard-docs           # Documentation
└── freedomguard-website        # Site web du projet
```

### 8.2 CI/CD

```
GitHub Actions Workflows :

┌─────────────────────────────────────────────────┐
│  Pull Request → Tests + Lint + Build Check      │
│  Main branch  → Build + Sign + Release (draft)  │
│  Tag/Release  → Build + Sign + Publish          │
│                                                 │
│  Android:                                       │
│  ├── Unit tests (JUnit5)                        │
│  ├── Instrumented tests (Espresso)              │
│  ├── Lint (ktlint)                              │
│  ├── Build APK (debug + release)                │
│  └── Publish → GitHub Releases + F-Droid        │
│                                                 │
│  iOS:                                           │
│  ├── Unit tests (XCTest)                        │
│  ├── Lint (SwiftLint)                           │
│  ├── Build (Xcode Cloud ou self-hosted mac)     │
│  └── Publish → TestFlight + App Store           │
│                                                 │
│  Windows:                                       │
│  ├── Unit tests                                 │
│  ├── Build (MSBuild + Gradle)                   │
│  ├── Sign (code signing certificate)            │
│  └── Publish → GitHub Releases + Winget         │
│                                                 │
│  KMP Shared:                                    │
│  ├── Unit tests (KMP test)                      │
│  ├── Integration tests                          │
│  └── Publish → Maven (for modules)              │
└─────────────────────────────────────────────────┘
```

### 8.3 Standards de Code

| Standard | Outil |
|----------|-------|
| Kotlin style | ktlint + detekt |
| Swift style | SwiftLint |
| C++ style | clang-format |
| Commit messages | Conventional Commits |
| Branch strategy | Git Flow (main, develop, feature/*, release/*) |
| Code review | Minimum 1 reviewer |
| Documentation | KDoc (Kotlin), DocC (Swift) |

---

*Ce document sera mis à jour au fur et à mesure de l'avancement du projet.*

# 📋 Spécifications Techniques — FreedomGuard

> **Version** : 0.1 (Draft)  
> **Date** : 19 Juin 2026  
> **Licence** : GPLv3 (Open Source, Copyleft — empêche la fermeture du code)

---

## 1. Vision du Produit

### 1.1 Mission
> **Libérer les personnes de leurs addictions numériques en fournissant un outil gratuit, open-source, robuste et cross-platform, fondé sur la science de la récupération dopaminergique.**

### 1.2 Principes Fondamentaux

| Principe | Description |
|----------|-------------|
| 🆓 **Gratuit pour toujours** | Le core product est et restera 100% gratuit |
| 🔓 **Open Source (GPLv3)** | Transparence totale, auditabilité, confiance |
| 🧠 **Fondé sur la science** | Protocole de 30 jours basé sur Dr. Anna Lembke |
| 🛡️ **Robuste par design** | Impossible (ou très difficile) à contourner |
| 🌍 **Cross-platform** | Android, iOS, Windows (macOS & Linux futurs) |
| 🔒 **Privacy-first** | Tout en local, pas de données envoyées à des serveurs |
| ❤️ **Empathique** | Pas de jugement, tolérant aux rechutes |

### 1.3 Nom du Projet
**FreedomGuard** — *"Garde ta liberté"*  
(Nom de travail — à valider avec la communauté)

---

## 2. Types d'Addictions Ciblées

| Type | Exemples | Méthode de Blocage |
|------|----------|-------------------|
| **Réseaux sociaux** | Instagram, TikTok, Twitter/X, Facebook, Reddit, YouTube | Blocage d'app + DNS |
| **Pornographie** | Sites pour adultes, applications | DNS filtering + catégories |
| **Jeux vidéo** | Jeux mobiles, Steam, consoles | Blocage d'app + limites horaires |
| **Gambling** | Paris en ligne, casinos | DNS + blocage d'app |
| **Shopping compulsif** | Amazon, Temu, etc. | Blocage d'app + DNS |
| **Messagerie compulsive** | WhatsApp, Discord (optionnel) | Limites horaires |
| **Streaming** | Netflix, YouTube, Twitch | Limites horaires + DNS |
| **Autre** | Personnalisable par l'utilisateur | Blocage d'app + URL + DNS |

---

## 3. Architecture Fonctionnelle

### 3.1 Vue d'Ensemble

```
┌─────────────────────────────────────────────────────────────────┐
│                      FreedomGuard App                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐       │
│  │ Recovery │  │ Blocking │  │ Account. │  │ Stats &  │       │
│  │  Engine  │  │  Engine  │  │  System  │  │ Insights │       │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘       │
│       │              │              │              │             │
│  ┌────┴──────────────┴──────────────┴──────────────┴────┐       │
│  │              Core Business Logic (KMP)               │       │
│  │     (Shared across Android, iOS, Windows)            │       │
│  └──────────────────────┬───────────────────────────────┘       │
│                         │                                       │
│  ┌──────────────────────┴───────────────────────────────┐       │
│  │           Platform Abstraction Layer                  │       │
│  ├───────────┬───────────┬──────────────────────────────┤       │
│  │  Android  │    iOS    │         Windows              │       │
│  │  Module   │  Module   │         Module               │       │
│  │           │           │                              │       │
│  │ • VPN     │ • Screen  │ • Windows Service            │       │
│  │   Service │   Time    │ • DNS Proxy                  │       │
│  │ • Access. │   API     │ • Firewall API               │       │
│  │   Service │ • Family  │ • Registry/ACL               │       │
│  │ • Device  │   Controls│ • Watchdog                   │       │
│  │   Admin   │ • MDM     │ • Browser Ext.               │       │
│  └───────────┴───────────┴──────────────────────────────┘       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 3.2 Modules Principaux

#### Module 1 : Recovery Engine (Moteur de Guérison)
Le cœur thérapeutique de l'application.

**Fonctionnalités :**
- **Programme de 30 jours** : Guide quotidien basé sur le protocole Lembke
  - Jour 1-7 : Phase de sevrage (messages de soutien, explications des symptômes)
  - Jour 8-21 : Phase d'ajustement (exercices de pleine conscience, activités alternatives)
  - Jour 22-30 : Phase de reset (réflexion, planification post-30 jours)
- **Compteur de streak** : Jours consécutifs sans rechute
- **Journal quotidien** : Humeur, envies, réflexions (tout en local, chiffré)
- **Contenu éducatif** : Articles sur la dopamine, neuroplasticité, témoignages
- **Exercices** : Respiration, méditation, gestion des envies
- **"Dopamine Menu"** : Activités alternatives saines suggérées
- **Tolérance à la rechute** : Pas de punition, encouragement à reprendre

**Protocole DOPAMINE intégré :**
| Étape | Fonctionnalité app |
|-------|-------------------|
| **D**ata | Questionnaire initial sur les habitudes |
| **O**bjectifs | Configuration des objectifs personnels |
| **P**roblèmes | Auto-évaluation des conséquences |
| **A**bstinence | Lancement du programme 30 jours avec blocage |
| **M**indfulness | Exercices quotidiens de pleine conscience |
| **I**nsight | Statistiques et réflexions hebdomadaires |
| **N**ext step | Plan post-30 jours (continuer ou modération) |
| **E**xpériment | Réintroduction graduelle contrôlée |

#### Module 2 : Blocking Engine (Moteur de Blocage)
La couche technique de protection.

**Niveaux de blocage :**

```
Niveau 1 — SOFT (Avertissement)
├── Notification de rappel quand app bloquée ouverte
├── Écran d'interception avec message de motivation
└── Délai de 10 secondes avant accès (friction)

Niveau 2 — MEDIUM (Blocage avec échappatoire)
├── App bloquée redirigée vers FreedomGuard
├── Accès possible avec code PIN + délai 5 min
└── Notification à l'accountability partner

Niveau 3 — HARD (Blocage sans échappatoire)
├── App complètement bloquée
├── Pas de code PIN possible pendant la période
├── Désinstallation impossible
└── Force-stop résistant
```

**Mécanismes de blocage par plateforme :**

| Mécanisme | Android | iOS | Windows |
|-----------|---------|-----|---------|
| **Blocage d'apps** | Accessibility Service + Overlay | Screen Time API (ManagedSettings) | Process monitoring + kill |
| **Blocage DNS** | Local VPN (VpnService) | MDM Profile / DNS config | DNS Proxy Service |
| **Blocage de sites** | VPN + DNS filter | Safari Content Blocker + DNS | Hosts file + Proxy + Extension |
| **Anti-désinstallation** | Device Admin + Overlay detection | FamilyControls (denyAppRemoval) | Service ACL + Watchdog |
| **Anti-force stop** | Foreground Service + restart | iOS gère automatiquement | Service auto-restart |
| **Blocage paramètres** | Overlay sur Settings | ManagedSettings restrictions | GPO / Registry protection |

#### Module 3 : Accountability System (Système de Responsabilité)
Le partenaire de responsabilité.

**Fonctionnalités :**
- **Lien de partenariat** : Inviter un ami/famille via un code unique
- **Notifications au partenaire** : Alertes si tentative de contournement
- **Rapport hebdomadaire** : Résumé anonymisé envoyé au partenaire
- **Appel d'urgence** : Bouton pour contacter le partenaire en cas de crise
- **Communication pair-à-pair** : Directe, chiffrée, pas de serveur central
- **Multi-partenaires** : Possibilité d'avoir plusieurs accountability partners

**Architecture communication :**
- Protocole pair-à-pair chiffré (E2E)
- Pas de serveur central (privacy-first)
- Options : 
  - Notifications push via Firebase/APNs (minimum de données)
  - Alternative : notifications par email (100% offline)

#### Module 4 : Statistics & Insights (Statistiques & Analyses)
Le tableau de bord de progrès.

**Données trackées (tout en local) :**
- Temps d'écran par app/catégorie
- Nombre de tentatives de blocage (combien de fois l'app a protégé)
- Streak actuel et historique
- Humeur quotidienne (auto-évalué)
- Heures les plus vulnérables (heatmap)
- Progrès dans le programme 30 jours

**Visualisations :**
- Graphique d'évolution sur 30/90/365 jours
- Heatmap horaire des envies
- Score de récupération (basé sur la durée d'abstinence)
- Comparaison semaine/semaine

---

## 4. Spécifications Anti-Contournement Détaillées

### 4.1 Philosophie
> **"L'addiction est une maladie du cerveau. En moment de faiblesse, l'utilisateur ESSAIERA de contourner la protection. Notre app doit être plus forte que l'envie."**

### 4.2 Système de Délai de Refroidissement (Cooling-Off)
Inspiré de Pluckeye, toute modification des paramètres de blocage est soumise à un délai :

| Action | Délai minimum | Configurable jusqu'à |
|--------|--------------|---------------------|
| Réduire le niveau de blocage | 24 heures | 72 heures |
| Supprimer une app de la blocklist | 24 heures | 72 heures |
| Désinstaller FreedomGuard | 48 heures | 7 jours |
| Désactiver le programme 30 jours | **Impossible** pendant le programme | - |
| Changer l'accountability partner | 48 heures | 7 jours |

### 4.3 Mesures Anti-Contournement par Plateforme

#### Android — Détail

```
Protection multi-couches :

Couche 1 : VPN Local (DNS Filtering)
├── Intercepte toutes les requêtes DNS
├── Bloque les domaines par catégorie
├── Blocklists : OISD, Energized, StevenBlack, + custom
├── Si VPN désactivé → notification alerte + re-activation auto
└── Monitoring constant via Foreground Service

Couche 2 : Accessibility Service
├── Détecte l'ouverture d'apps bloquées
├── Affiche overlay de blocage instantané
├── Détecte tentatives d'aller dans Settings > Apps
├── Bloque la navigation vers "Désinstaller" pour FreedomGuard
└── Détecte les tentatives de changer DNS dans Settings

Couche 3 : Device Administrator
├── Empêche la désinstallation directe
├── Requiert désactivation d'admin avant désinstallation
├── Désactivation soumise au délai de refroidissement
└── Notification à l'accountability partner

Couche 4 : Foreground Service Persistant
├── Notification permanente "FreedomGuard actif"
├── Auto-restart si processus tué
├── Boot receiver pour restart au démarrage
├── Battery optimization exclusion demandée à l'utilisateur
└── Alarm Manager pour vérification périodique

Couche 5 : Monitoring Intégrité
├── Vérifie que le VPN est actif toutes les 30 secondes
├── Vérifie que l'Accessibility Service est actif
├── Si détection de désactivation → re-activation + alerte
└── Hash des fichiers de config pour détecter tampering
```

#### iOS — Détail

```
Protection multi-couches :

Couche 1 : Screen Time API (FamilyControls)
├── Authorization via FamilyControls
├── store.application.denyAppRemoval = true
├── ManagedSettingsStore pour bloquer apps spécifiques
├── Shield configuration personnalisée (écran de blocage)
└── Fonctionne même après reboot

Couche 2 : ManagedSettings Framework
├── Blocage d'apps par token (privacy-preserving)
├── Restrictions de contenu web
├── Blocage de certains paramètres système
└── Limites de temps par catégorie d'app

Couche 3 : Network Extension (si approuvé par Apple)
├── Content Filter Provider
├── Filtrage DNS au niveau système
├── Fonctionne en background
└── Nécessite entitlement spécial Apple

Couche 4 : Profil MDM Self-Hosted (Optionnel)
├── Pour utilisateurs avancés
├── Profil de restriction installé sur l'appareil
├── Nécessite un serveur MDM léger
├── Empêche la suppression d'apps et la modification de settings
└── Alternative : MicroMDM open source
```

#### Windows — Détail

```
Protection multi-couches :

Couche 1 : Windows Service (SYSTEM)
├── Tourne en tant que NT AUTHORITY\SYSTEM
├── Recovery options: auto-restart on failure
├── ACLs restrictives sur le service
├── Monitoring des processus bloqués
└── Kill automatique des processus dans la blocklist

Couche 2 : DNS Proxy Service
├── Proxy DNS local (127.0.0.1:53)
├── Configuration réseau automatique
├── Filtrage par catégorie via blocklists
├── Fallback sur DNS sécurisé (DoH) pour le trafic légitime
└── Protection de la config DNS (monitoring des changements)

Couche 3 : Watchdog Service
├── Service séparé qui surveille le service principal
├── Si service principal arrêté → restart immédiat
├── Si fichiers modifiés → restauration depuis backup
├── Si registre modifié → restauration
└── Le watchdog surveille le service ET vice-versa

Couche 4 : Firewall & Host Filtering
├── Windows Firewall rules via API
├── Modification du fichier hosts (avec protection)
├── WFP (Windows Filtering Platform) pour filtrage avancé
└── ACLs sur le fichier hosts

Couche 5 : Protection Désinstallation
├── Désinstalleur protégé par délai de refroidissement
├── Nécessite code accountability partner OU délai 48h
├── Pas d'entrée dans Add/Remove Programs standard
├── Désinstallation via CLI spécial uniquement
└── Log de toutes les tentatives
```

---

## 5. Protocole de Guérison Intégré

### 5.1 Programme "30 Jours de Liberté"

```
JOUR 0 : ENGAGEMENT
├── Questionnaire : type d'addiction, sévérité, déclencheurs
├── Choix du niveau de blocage (Soft / Medium / Hard)
├── Configuration des apps/sites à bloquer
├── Invitation d'un accountability partner (optionnel mais recommandé)
├── Lecture : "Qu'est-ce que la dopamine et pourquoi ça compte"
└── ENGAGEMENT SIGNÉ (symbolique, confirmer 30 jours)

SEMAINE 1 : LE SEVRAGE (Jours 1-7)
├── Message quotidien : "Ce que tu ressens est NORMAL"
├── Explication des symptômes de sevrage
├── Exercice de respiration 4-7-8 (matin et soir)
├── "Dopamine Menu" : 3 activités alternatives suggérées/jour
├── Check-in humeur quotidien
└── Blocage : MAXIMUM (pas de modifications possibles)

SEMAINE 2 : L'AJUSTEMENT (Jours 8-14)
├── Message : "Le plus dur est passé, continue"
├── Introduction à la pleine conscience
├── Exercice : identifier tes 3 déclencheurs principaux
├── Journal de gratitude quotidien
├── Check-in avec accountability partner
└── Statistiques : combien de tentatives bloquées

SEMAINE 3 : LA TRANSFORMATION (Jours 15-21)
├── Message : "Ton cerveau se recâble"
├── Exercice : planifier ta semaine sans écran
├── Réflexion : qu'est-ce qui a changé dans ta vie ?
├── Article : neuroplasticité et nouvelles habitudes
├── Challenge : activité en plein air
└── Statistiques : comparaison semaine 1 vs semaine 3

SEMAINE 4 : LE RESET (Jours 22-28)
├── Message : "Tu es presque libre"
├── Exercice : écrire une lettre à ton futur soi
├── Réflexion : comment maintenir les changements
├── Planification post-30 jours
├── Check-in approfondi avec accountability partner
└── Statistiques : évolution complète

JOURS 29-30 : LA DÉCISION
├── Célébration du parcours
├── Questionnaire de réévaluation
├── Choix : 
│   ├── Continuer l'abstinence totale
│   ├── Réintroduction contrôlée (limites horaires)
│   └── Nouveau programme 90 jours
├── Rapport complet de récupération
└── Badge "30 jours de liberté" 🏅
```

### 5.2 Gestion des Rechutes

```
SI RECHUTE DÉTECTÉE :
├── PAS de jugement, PAS de reset du compteur principal
├── Message empathique : "Une rechute n'efface pas tes progrès"
├── Compteur secondaire : "Depuis la dernière rechute"
├── Compteur principal : "Total de jours avec effort"
├── Proposer un check-in avec accountability partner
├── Exercice de réflexion : qu'est-ce qui a déclenché la rechute ?
├── Renforcement du blocage si l'utilisateur le souhaite
└── Redémarrage doux du programme (pas depuis le jour 0)
```

---

## 6. Spécifications de l'Interface Utilisateur

### 6.1 Principes de Design

| Principe | Application |
|----------|-------------|
| **Calme** | Couleurs apaisantes, pas de stimulation visuelle excessive |
| **Empathique** | Ton bienveillant, messages de soutien |
| **Simple** | Maximum 3 clics pour n'importe quelle action |
| **Accessible** | Support lecteur d'écran, tailles de police ajustables |
| **Dark mode** | Thème sombre par défaut (moins stimulant) |
| **Multilingue** | Français, Anglais, Espagnol, Arabe (v1) |

### 6.2 Écrans Principaux

1. **Dashboard** — Vue d'ensemble
   - Streak actuel (grand, centré)
   - Progression du programme 30 jours (barre de progrès)
   - Message du jour
   - Bouton "SOS" (urgence envie)

2. **Programme** — Guide quotidien
   - Contenu du jour (article, exercice, réflexion)
   - Check-in humeur
   - Journal

3. **Blocage** — Configuration
   - Liste des apps/sites bloqués
   - Niveau de blocage actuel
   - Historique des tentatives bloquées
   - Délai de refroidissement si modification

4. **Partenaire** — Accountability
   - Statut du partenaire
   - Messages/notifications
   - Rapport partagé

5. **Stats** — Statistiques
   - Graphiques de progrès
   - Heatmap des envies
   - Score de récupération

6. **Écran de Blocage** (overlay quand app bloquée)
   - Message de motivation aléatoire
   - Compteur de streak
   - Rappel de pourquoi tu fais ça (message personnalisé par l'utilisateur)
   - Bouton "Respirer" (exercice rapide 1 min)
   - **PAS** de bouton "Continuer quand même" en mode Hard

---

## 7. Données et Vie Privée

### 7.1 Principes de Privacy

| Règle | Détail |
|-------|--------|
| **Tout en local** | Toutes les données restent sur l'appareil |
| **Pas de télémétrie** | Aucune donnée envoyée à des serveurs |
| **Chiffrement** | Journal et données sensibles chiffrés (AES-256) |
| **Pas de compte** | Pas de création de compte requise |
| **Export/suppression** | L'utilisateur peut exporter ou supprimer ses données à tout moment |
| **Accountability** | Communication E2E chiffrée, données minimales |

### 7.2 Données Stockées

| Donnée | Stockage | Chiffrée | Exportable |
|--------|----------|----------|------------|
| Apps/sites bloqués | Local | Non | Oui |
| Streak/compteurs | Local | Non | Oui |
| Journal quotidien | Local | **Oui** (AES-256) | Oui |
| Check-ins humeur | Local | **Oui** | Oui |
| Stats d'usage | Local | Non | Oui |
| Config accountability | Local | **Oui** | Non |
| Logs de blocage | Local | Non | Oui |

---

## 8. Distribution

### 8.1 Canaux de Distribution

| Plateforme | Canal | Raison |
|-----------|-------|--------|
| Android | **F-Droid** (principal) | Écosystème open source, pas de restrictions |
| Android | **APK direct** (site web) | Liberté totale, pas de gatekeeping |
| Android | Google Play (si possible) | Audience maximale (mais risque de rejet à cause des permissions) |
| iOS | **App Store** | Seul canal possible sur iOS |
| Windows | **GitHub Releases** | Standard open source |
| Windows | **Winget / Chocolatey** | Package managers Windows |
| Windows | Site web (installer .exe) | Accessibilité maximale |

### 8.2 Contraintes App Stores

| Store | Risque | Mitigation |
|-------|--------|------------|
| Google Play | Rejet pour usage d'Accessibility Service | Justifier l'usage légitime, distribuer aussi sur F-Droid |
| App Store | Entitlement FamilyControls requis | Demander l'approbation Apple en avance, démontrer l'usage légitime |
| F-Droid | Aucun | ✅ Parfait pour notre cas d'usage |

---

## 9. Stack Technologique Recommandée

### 9.1 Architecture

```
┌────────────────────────────────────────────────────┐
│                  Shared (KMP)                      │
│  ┌──────────────────────────────────────────────┐  │
│  │  • Domain Models (Kotlin)                    │  │
│  │  • Business Logic / Use Cases                │  │
│  │  • Repository Interfaces                     │  │
│  │  • Recovery Protocol Engine                  │  │
│  │  • Blocklist Management                      │  │
│  │  • Statistics Engine                         │  │
│  │  • Encryption Utils                          │  │
│  └──────────────────────────────────────────────┘  │
├────────────────────────────────────────────────────┤
│              Platform Implementations              │
│  ┌──────────┐  ┌──────────┐  ┌─────────────────┐  │
│  │ Android  │  │   iOS    │  │    Windows      │  │
│  │          │  │          │  │                 │  │
│  │ Kotlin   │  │ Swift    │  │ Kotlin/JVM +   │  │
│  │ Jetpack  │  │ SwiftUI  │  │ Compose Desktop│  │
│  │ Compose  │  │          │  │ + C++ Service  │  │
│  │          │  │ Screen   │  │                 │  │
│  │ VPN      │  │ Time API │  │ Windows Service │  │
│  │ Service  │  │ Family   │  │ WFP Driver     │  │
│  │ Access.  │  │ Controls │  │ DNS Proxy      │  │
│  │ Service  │  │ Network  │  │                 │  │
│  │ Device   │  │ Ext.     │  │                 │  │
│  │ Admin    │  │          │  │                 │  │
│  └──────────┘  └──────────┘  └─────────────────┘  │
└────────────────────────────────────────────────────┘
```

### 9.2 Technologies

| Composant | Technologie | Justification |
|-----------|-------------|---------------|
| **Shared Logic** | Kotlin Multiplatform | 60-90% code partagé, mature, Google-backed |
| **Android UI** | Jetpack Compose | Standard moderne Android |
| **Android Services** | Kotlin + Android SDK | VpnService, AccessibilityService, DeviceAdmin |
| **iOS UI** | SwiftUI | Standard moderne iOS |
| **iOS APIs** | Swift + FamilyControls/ManagedSettings | APIs Apple officielles |
| **Windows UI** | Compose Multiplatform Desktop | Partage de code avec Android |
| **Windows Service** | C++ ou Rust | Performance, accès système bas niveau |
| **DNS Filtering** | Blocklists (OISD, StevenBlack, custom) | Standard de l'industrie |
| **Local Storage** | SQLDelight (KMP) | Base de données cross-platform |
| **Encryption** | AES-256-GCM (platform native) | Standard de sécurité |
| **P2P Communication** | WebRTC ou Protocole custom | Accountability partner sans serveur |
| **Build System** | Gradle (KMP) + Xcode + CMake | Standards par plateforme |
| **CI/CD** | GitHub Actions | Open source friendly |

---

## 10. Exigences Non-Fonctionnelles

| Catégorie | Exigence | Cible |
|-----------|----------|-------|
| **Performance** | Démarrage de l'app | < 2 secondes |
| **Performance** | Impact batterie (Android VPN) | < 5% additionnel |
| **Performance** | Latence DNS filtering | < 10ms additionnel |
| **Fiabilité** | Uptime du service de blocage | 99.9% (tant que l'appareil est allumé) |
| **Fiabilité** | Restart après crash | < 5 secondes |
| **Fiabilité** | Restart après reboot | Automatique |
| **Sécurité** | Chiffrement données sensibles | AES-256-GCM |
| **Sécurité** | Communication accountability | E2E chiffré |
| **Accessibilité** | Support lecteur d'écran | WCAG 2.1 AA |
| **Accessibilité** | Langues supportées (v1) | FR, EN, ES, AR |
| **Taille** | Taille de l'APK Android | < 15 MB |
| **Taille** | Taille de l'app iOS | < 20 MB |
| **Taille** | Taille de l'installeur Windows | < 30 MB |

---

*Ce document sera mis à jour au fur et à mesure du développement.*

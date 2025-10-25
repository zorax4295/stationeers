# Système de Sas – Modular Consol
## Description

Ce système de sas automatisé permet de gérer l’ouverture et la fermeture des portes, la ventilation et la sécurité du sas de manière autonome. Il utilise des appareils du mod Modular Consol pour contrôler le sas et superviser les conditions de pression et de sécurité.

## Appareils utilisés par le programme “Sas Core”
### Portes et ventilation

- Porte intérieure

- Porte extérieure

- Ventilateur intérieur

- Ventilateur extérieur

### Capteurs

- Capteur de gaz

### Boutons et interrupteurs

- Bouton SOS

- Interrupteur Maintenance

- Bouton aquitter SOS

### Éclairage

- Flashlight

- Light Round

### Affichages

- Jauge de pression du réservoir

- Jauge de pression du sas

### Housings

- Housing Accès

- Housing Contrôle

## Fonctionnement du Sas

Le programme Sas Core constitue le noyau opérationnel du sas. Il gère toutes les actions nécessaires pour assurer un fonctionnement sûr et fluide, mais ne prend pas de décision sur l’autorisation de démarrage du sas, qui est gérée par le programme de contrôle.

### Cycle d’ouverture et fermeture

Le sas fonctionne selon deux cycles : Inter→Exter ou Exter→Inter, contrôlés par le système interne (sensCycle).

Sas Core verrouille et déverrouille les portes automatiquement pour éviter toute ouverture simultanée et fuite d’air.

Chaque cycle est exécuté étape par étape, assurant que la pression est équilibrée avant d’ouvrir une porte.

### Gestion de la pression

Les ventilateurs intérieur et extérieur sont activés pour pressuriser ou dépressuriser le sas selon le cycle en cours.

La pression est surveillée en continu pour synchroniser l’ouverture des portes avec le niveau de pression correct.

### Éclairage

Flashlight et l’éclairage du sas sont activés automatiquement lors du cycle d’utilisation pour guider le passage et signaler l’état du sas.

### Maintenance et interruptions

Si l’interrupteur Maintenance est activé et que la carte d’accès autorise le mode maintenance, le système bascule en mode maintenance, déverrouillant toutes les portes et ventilateurs et les arrêtant.

Le bouton SOS peut interrompre le cycle en cours et bloquer temporairement le fonctionnement du sas.

Le bouton aquitter SOS permet de quitter l’état d’interruption et de revenir à l’état initial.

### Housings

Housing Accès : contrôle l’accès aux commandes du sas pour les utilisateurs.

Housing Contrôle : n’agit pas directement dans ce programme, il est utilisé pour autoriser ou bloquer le démarrage du sas selon les conditions de sécurité (pression correcte, gaz nocif, etc.).

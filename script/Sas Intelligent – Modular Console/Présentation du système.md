# Sas Intelligent – Modular Console
## Description

Ce système de sas automatisé permet de gérer l’ouverture et la fermeture des portes, la ventilation et la sécurité du sas de manière autonome. Il utilise des appareils du mod Modular Consol pour contrôler le sas et superviser les conditions de pression et de sécurité.

## Le système est composé de trois programmes indépendants :

- Sas Core : gère le fonctionnement interne du sas (portes, ventilation, éclairage).

- Contrôle : vérifie les conditions de sécurité avant le démarrage.

- Accès : gère les autorisations utilisateur via carte d’accès.

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

- Bouton acquitter SOS

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

## Fonctionnement du Programme de Contrôle

Le programme de contrôle gère la sécurité et les conditions de démarrage du sas. Il ne gère pas directement les portes ou la ventilation (c’est le rôle de Sas Core), mais décide si celui-ci peut démarrer et si les conditions sont sûres pour un cycle.

### Vérifications et conditions

- Autorisation de démarrage :

  - Le programme vérifie que le cycle peut démarrer via l’interrupteur de cycle et la carte d’accès.

  - Il bloque le démarrage si un signal SOS est actif.

- Analyse du sas et du réservoir :

  - Mesure la pression, la température, et les différents ratios de gaz et polluants à l’intérieur du sas et du réservoir.

  - Conditions du réservoir : pression entre 10 et 45 MPa, température autour de 20 °C, gaz et polluants dans les limites de sécurité.

  - Conditions du sas : pression proche de 100 kPa, température autour de 20 °C, gaz et polluants dans les limites de sécurité.

- Prêt pour démarrage :

  - Si toutes les conditions sont respectées, le cycle est marqué comme prêt, et une diode verte (Diode Cycle Prêt) s’allume.

  - Si les conditions ne sont pas remplies, la diode devient rouge et le cycle est bloqué.

### Interaction avec Sas Core

- Quand le cycle est prêt et que tous les contrôles sont validés :

  - Le programme active le démarrage (IC.Setting = 1) qui permet à Sas Core d’exécuter le fonctionnement du sas (portes, ventilateurs, éclairage).

- Si une condition échoue (pression, gaz, SOS, accès) :

  - Le programme bloque le démarrage et Sas Core ne peut pas démarrer son cycle.

## Fonctionnement du Programme d’Accès

Le programme d’accès gère l’autorisation d’entrée au sas à l’aide d’un lecteur de carte.
Chaque carte correspond à une catégorie d’utilisateur représentée par une couleur.
Le programme compare la carte insérée avec les autorisations définies et détermine si l’accès est accordé ou refusé.

### Principe de fonctionnement

Lorsqu’une carte est insérée, le programme identifie sa couleur.
Il vérifie ensuite si cette carte est autorisée pour un accès normal ou pour un accès maintenance.
Selon le résultat, le lecteur de carte affiche une couleur indiquant le niveau d’accès accordé.

### Indicateurs visuels

Le lecteur de carte affiche une couleur selon le type d’accès accordé :

🟢 Vert → Carte acceptée (accès normal)

🟡 Jaune → Carte acceptée avec accès maintenance

🔴 Rouge → Carte refusée




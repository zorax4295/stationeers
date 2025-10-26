# Guide d’installation du Sas
## 🧾 Introduction

Ce fichier explique comment mettre en place le sas à air permettant de faire transiter une personne entre l’extérieur et la base.
Il décrit les étapes essentielles d’installation et de câblage des différents modules et appareils nécessaires au fonctionnement du système : alimentation électrique, liaison de données entre les programmes (`Core`, `Control`, `Access`), et configuration des noms requis.

## ⚡ Câblage énergétique

Tous les appareils du sas (portes, ventilateurs, capteurs, IC Housing, voyants, etc.) doivent être alimentés en **aval d’un APC ou d’un transformateur**.
Cela garantit une alimentation stable et contrôlée.

> [!IMPORTANT]
> Aucune connexion directe sur le réseau principal n’est autorisée, car cela provoquerait des conflits avec d’autres programmes.
> Chaque circuit de sas doit être isolé électriquement du réseau global.

## 📡 Câblage de données

Le câblage de données relie les différents modules logiques (`Core`, `Control`, `Access`) ainsi que les capteurs et actionneurs du sas.
Chaque IC doit être connecté conformément au tableau suivant.
Les noms indiqués dans la colonne Nom requis doivent être appliqués exactement comme tels dans le jeu pour que les programmes fonctionnent correctement.

### 🧠 Programme Core

| Appareil | Commentaire | Connexion | Nom de l'appareil |
| :------: | :---------: | :-------: | :---------------: |
| Porte intérieure | Porte menant vers la base | Pin 0 | ———— |
| Porte extérieure | Porte menant vers l’extérieur | Pin 1 | ———— |
| Ventilateur intérieur | ———— | Pin 2 | ———— |
| Ventilateur extérieur | ———— | Pin 3 | ———— |
| Capteur de gaz du sas | ———— | Pin 4 | ———— |
| Housing Access | Connexion vers le programme Access | Pin 5 | ———— |
| Bouton SOS | Déclenche une alarme et interrompt le sas | Batch name | SOS |
| Interrupteur Maintenance | Active le mode maintenance | Batch name | Maintenance |
| Bouton Acquittement SOS | Réinitialise l’état SOS | Batch name | Acquiter SOS |
| Flashing Light | Indication visuelle de fonctionnement | Batch | ———— |
| Light round | Éclaire le sas | Batch | ———— |
| Housing Control | Connexion vers le programme control | Batch name | IC Housing control |

### 🧩 Programme Control

| Appareil | Commentaire | Connexion | Nom de l'appareil |
| :------: | :---------: | :-------: | :---------------: |
| Housing Access | Connexion vers le programme Access | Pin 0 | ———— |
| Housing Core | Connexion vers le programme Core | Pin 1 |	———— |
| Capteur de gaz du sas | Vérifie la pression du sas | Pin 2 |	———— |
| Pipe analiser du tank |	Analyse la composition du tank | Pin 3 |	———— |
| Capteur de gaz de la salle intérieur | Analyse la composition de la salle intérieur | Pin 4 |	———— |
| Diode Cycle Prêt | Indique si le sas peut être lancé | Batch name | Diode Cyle Pret |
| levier de lancement du cycle | Lance un cycle de sas | Batch name |	cycle sas |
| Gauge pression tank | Mesure la pression du tank | Batch name | Pressure Tank |
| Gauge pression sas | Mesure la pression du sas | Batch name | Pressure sas |

### 🪪 Programme Access

| Appareil | Commentaire | Connexion | Nom de l'appareil |
| :------: | :---------: | :-------: | :---------------: |
| Access Card Reader | Permet la lecture des cartes | Batch name | Access Card Reader |

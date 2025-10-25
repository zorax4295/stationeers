# Paramètres optionnels

Ce fichier présente les paramètres que l’utilisateur peut modifier librement dans le programme afin d’adapter le comportement du sas à son environnement ou à ses préférences.
Ces modifications ne sont pas obligatoires, mais permettent d’ajuster la pression ou le sens initial du cycle.

## 🔧 Paramètres disponibles programme [sas core](sas%20core/instruction.xml)
### @PressureInter

**Valeur par défaut :** `100 kPa`

**Description :** Définit la pression de référence intérieure (côté base).

**Utilité :** à ajuster si votre base fonctionne à une pression différente.

**Exemple :**

```vb
define pressureinter 100
```

### @PressureExter

**Valeur par défaut :** `0 kPa`

**Description :** Définit la pression de référence extérieure (côté extérieur du sas).

**Utilité :** à ajuster si vous évoluez dans une atmosphère légèrement pressurisée (ex. sur une planète avec atmosphère).

**Exemple :**
```vb
define pressureexter 25
```

### @sensCycle

**Valeur par défaut :** `0`

**Description :** Définit le **_sens initial du premier cycle_** du sas.

**Valeurs possibles :**

  - 0 → Cycle Intérieur → Extérieur

  - 1 → Cycle Extérieur → Intérieur

**Utilité :** permet de choisir le sens de fonctionnement par défaut après un redémarrage.
Le programme alterne automatiquement le sens après chaque cycle complet.

> [!IMPORTANT]
> Ses trois constante son déjà intégré au programme elle ne doivent pas être rajouter mais modifié

> [!WARNING]
> Seules ces trois constantes sont destinées à être modifiées par l’utilisateur.
> Les autres éléments du code gèrent la logique interne et ne doivent pas être modifiés sans connaissance approfondie du programme.
> Après toute modification, redémarrez l’IC Housing concerné pour appliquer les changements.


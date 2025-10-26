> [!IMPORTANT]
> Les constante son déjà intégré au programme elle ne doivent pas être rajouter mais modifié.

> [!WARNING]
> Seules ces constantes sont destinées à être modifiées par l’utilisateur.
> Les autres éléments du code gèrent la logique interne et ne doivent pas être modifiés sans connaissance approfondie du programme.
> Après toute modification, redémarrez l’IC Housing concerné pour appliquer les changements.

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

## Paramètres disponibles programme [Contrôle](controle%20sas/instruction.xml)

Ces constantes influencent principalement les valeurs de référence utilisées pour l’affichage, les tests de conditions et la supervision du système.

### @PressureInterMax

**Valeur par défaut :** `300 kPa`

**Rôle :** Définit la valeur maximale affichée sur la jauge de pression du sas.

**Utilité :** Cette constante est purement esthétique — elle sert uniquement à l’échelle d’affichage de la jauge.

**Personnalisation :**

  - Peut être abaissée à la pression cible du sas (ex. 100 kPa) pour un affichage “plein” lorsque le sas est à pression normale.

  - Ou conservée à 300 kPa pour indiquer la pression maximale que la structure peut supporter.

**Exemple :**
```vb
define pressureintermax 300
```

(La jauge affichera 100 % lorsque le sas atteindra 100 kPa.)

### @PressureTarget

**Valeur par défaut :** `100 kPa`

**Rôle :** Définit la pression cible du sas, utilisée dans la fonction testCycleRoom() pour vérifier si la salle est stable avant le démarrage du cycle.

**Utilité :** Cette constante affecte directement la logique du programme :
le cycle ne démarre que si la pression ambiante est comprise dans une plage de ±2 kPa autour de cette valeur.

**Exemple :**
```vb
define pressuretarget 95
```

(Le sas sera considéré prêt si la pression est comprise entre 93 et 97 kPa.)

### @PressureTank

**Valeur par défaut :** `45 MPa`

**Rôle :** Définit la pression maximale autorisée pour le réservoir.

**Utilisée à la fois :**

  - dans la fonction testCycleSas() pour vérifier la sécurité du réservoir,

  - et comme valeur de référence pour la jauge de pression du réservoir.

**Utilité :** Cette constante influence la sécurité du système — si la pression dépasse ce seuil, le cycle ne sera pas autorisé.

**Personnalisation :**

À ajuster selon la pression de service réelle de vos réservoirs.

**Exemple :**
```vb
define pressuretank 45000
```

### @TemperatureTarget

**Valeur par défaut :** `20 °C`

**Rôle :** Définit la température cible de référence pour le sas et le réservoir.
Utilisée dans les fonctions testCycleSas() et testCycleRoom() pour vérifier que la température mesurée reste dans une plage de ±1 °C autour de cette valeur.

**Utilité :** Cette constante influence directement la logique de validation du cycle — le cycle ne pourra démarrer que si la température du sas et du réservoir est proche de cette valeur.

**Personnalisation :**

Peut être ajustée selon la température de fonctionnement de votre base.

Exemple :
```vb
define temperaturetarget 293
```

(Le sas sera considéré prêt si la température est comprise entre 21 °C et 23 °C.)

## Paramètres disponibles programme [Access Control](access%20Control/instruction.xml)

### `@acceditationBlanc`, `@acceditationVert`, `@acceditationJaune`, `@acceditationRose`, `@acceditationNoir`

**Valeurs possibles :**

  - 0 → Aucun accès

  - 1 → Accès normal

  - 2 → Accès maintenance (inclut aussi l’accès normal)

**Rôle :**

Ces constantes définissent le niveau d’autorisation attribué à chaque couleur de carte.
Elles permettent à l’utilisateur de déterminer quels types d’accès sont accordés pour chaque badge.

**Principe :**

Le programme vérifie la carte insérée dans le lecteur :

  - 0 → Carte refusée

  - 1 → Accès normal autorisé

  - 2 → Accès maintenance (fonctionnement normal + maintenance)

**Personnalisation :**

Ces valeurs peuvent être modifiées selon les besoins.

Exemple :
```vb
define acceditationblanc 1  # Accès normal
define acceditationnoir 2   # Accès normal + maintenance
```

> [!NOTE]
> Limitation connue :
> 
> Si deux cartes sont insérées en même temps dans deux lecteurs différents,
> le système interprète cela comme une erreur et refuse l’accès,
> même si les deux cartes sont valides.


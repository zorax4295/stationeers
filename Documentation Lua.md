# Variable :
Les variable en lua doivent être déclarer exemple :
```lua
a=0
```
Par défaut les varibale son déclarer global pour les déclarer local il faut le précisé exemple :
```lua
local a=0
```
les variable doivent d'abord être déclarer avant d'être utiliser. un exemple de config mauvaise :
```lua
b = a
local a = 0  -- ❌ b est nil ici
```
Liste des déclaration possible :
| Valeur        | Type        | Description                                      |
|--------------|------------|--------------------------------------------------|
| a = nil      | nil        | Absence de valeur (par défaut si non initialisée)|
| a = 1        | number     | Entier                                           |
| a = 3.14     | number     | Nombre flottant                                  |
| a = "hello"  | string     | Chaîne de caractères                             |
| a = true     | boolean    | Booléen                                          |
| a = {1,2,3}  | table      | Table (structure de données)                     |

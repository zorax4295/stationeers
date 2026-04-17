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

# Lecture/Ecriture [Doc officiel](https://orbitalfoundrymodteam.github.io/StationeersLuaDocs/api/device-io.html)
Pour lire une valeur nous utilison **ic.read(device, logicType)** exemple :
```lua
local temp = ic.read(0, LT.Temperature)
```
Pareil pour l'écriture d'une valeur avec **ic.write(device, logicType, value)** exemple :
```lua
ic.write(0, LT.On, 1)
```


# Les table :
## Déclaration de base :
exemple de table avec valeurs initiales :
```lua
table = {10, 20, 30}
print(t[1])  -- 10
print(t[2])  -- 20
```
exemple de table avec clés personnalisées :
```lua
local table = {name="Light", pin=0, state=true}
print(table.name)  -- Light
print(table["pin"]) -- 0
```
Son utilisation peut se faire avec **table.key** ou **table["key"]**
> [!TIP]
> A savoir les deux exemple de table peuvent être mélanger
## Tableaux imbriquée :
### Table indexée numériquement :
```lua
local devices = {
  {name="porte_interieur", open=nil},   -- index 1
  {name="porte_exterieur", open=nil},   -- index 2
  {name="light", on=nil}                -- index 3
}
```
Chaque élément a un indice numérique automatique (1, 2, 3…)<br>
Exemple pour acceder à un élément spécifique :
```lua
print(devices[1].name)  -- Affiche "porte_interieur"
print(devices[2].open)  -- Affiche nil
```
### Table indexée par string
```lua
local devices = {
  porte_interieur = {open=nil, lock=nil},
  porte_exterieur = {open=nil},
  light = {on=nil}
}
```
Chaque élément a une clé string ("porte_interieur", "porte_exterieur", "light")<br>
Exemple pour acceder à un élément spécifique :
```lua
print(devices.porte_interieur.open)  -- Affiche nil (état d'ouverture)
print(devices.porte_interieur.lock)  -- Affiche nil (état de verrouillage)
```

# Enumerations :
Les énumeration permette d'exposer les variable des appareil, lua n'a pas une syntaxe précise mais il faut garder chaque argument dans le bonne ordre et preciser quand ses un LogicType un LogicSlotType ect.<br>
Liste des logic type :
```lua
local LT  = ic.enums.LogicType         -- On, Off, Temperature, Pressure, ...
local LBM = ic.enums.LogicBatchMethod   -- Average, Sum, Minimum, Maximum
local LST = ic.enums.LogicSlotType      -- Occupied, Quantity, Charge, ...
local LRM = ic.enums.LogicReagentMode   -- TotalContents, ...
local DB = ic.const.BASE_UNIT_INDEX  -- Equivalent a db en ic10
```
exemple d'utilisation :
```lua
local LT = ic.enums.LogicType
print("Script initialized")

while true do
  local switchState = ic.read(1, LT.Open)
  ic.write(0, LT.On, switchState)
  sleep(0)
end
```
Dans se script pour l'ecriture ou la lecture le 2ème argument est toujour le LogicType ect mais il faut exposer le LogicType sinon le script ne le vois pas
> [!TIP]
> A savoir la variable LT sert a reutiliser facilement le Logictype ses plus compacte que d'utiliser "ic.enums.LogicType" partout

#Convertion de température :
Il est possible en lua de convertire une unité de température en une autre via :
```lua
util.temp(value, from, to)
```
Unités : « K » (Kelvin), « C » (Celsius), « F » (Fahrenheit). Insensible à la casse.
```lua
-- Stationeers sensors report Kelvin — convert to Celsius
local tempK = ic.read(0, ic.enums.LogicType.Temperature)
local tempC = util.temp(tempK, "K", "C")
print(tempC)  -- 21.85

-- Celsius to Fahrenheit
local tempF = util.temp(tempC, "C", "F")
print(tempF)  -- 71.33

-- Fahrenheit back to Kelvin
local tempK2 = util.temp(tempF, "F", "K")
print(tempK2)  -- 295.0
```
> [!NOTE]
> Le paramètre **from** est par défaut "K" et **to** par défaut "C", donc util.temp(295) est un raccourci rapide Kelvin → Celsius.

# Message direct
## Envoyer un message :
```lua
ic.net.send("Housing - Larre Hydroponic storage", "alert", "Hello World!")
```
syntaxe : ic.net.send(ic.net.send(target, tag, value))
la target peut soit être l'id de la cible ou alors son nom en string et la value peut être soit
- boolean
- number
- string
- table
## Recevoir un message
Pour commencer il faut créer la function qui va executer le code une fois le message reçus :
```lua
local function onAlert(fromId, fromName, payload)
    print("Message reçu de " .. fromName)
    print("Contenu : " .. tostring(payload))
end
```
Ensuite il faut s'enregistrer pour ecouter en gros pour faire un simple par défaut l'ic housing n'ecoute rien il faut enregistrer un tag sur la liste d'écoute exemple :
```lua
ic.net.listen("alert", onAlert)
```
Cette commande ecoute tout les message aillent le tag "alert" si un autre ic hosuing envoie un message au notre avec le tag "info" et qu'il ne ses pas enregistrer alors tout les message aillant le tag "info" seron tout simplement ignoré puisque notre ic housing ne les ecoute pas.
Pour arrêter d'écouter des message il faut se désanregistrer en specifiant le tag et nil exemple :
```lua
ic.net.listen("alerts", nil)
```

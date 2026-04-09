# Déclaration d’écrans en une ligne avec structure centralisée et paramètres UI auto-générés (accès simplifié aux propriétés)
```lua
-- renvoie les parametre des ecran dans la table des ecran
local function create_screen(name_screen)
    local surface = ss.ui.surface(name_screen)
    return {
        surface = ss.ui.surface(name_screen),
        activate = function()
            ss.ui.activate(name_screen)
        end,
    }
end
-- liste des ecran
local screens = {
    main = create_screen("main"), -- obtien la liste des paramtre de main
    temp = create_screen("test")
}
-- Recupere la taille physique de l'ecran
W = screens.main.surface:size().w
H = screens.main.surface:size().h
```
## explication du script
Regardon la liste des ecran, dedans nous y créeons une table puis y ajoutant un ecran avec son nom.
Maintenant grace a la function create_screen elle nous permet de créer automatiquement des parametre pour chaque ecran que nous déclarons dans la table.
Enfin la taille physique de l'ecran est recuperer tout en bas puis stocker dans les variables W pour la longueur et H pour la hauteur
## Syntaxe d’utilisation des écrans :
### Activation d’un écran
Syntaxe :
```lua
screens.<nom_ecran>.activate()
```
### Accès à la surface d’un écran
Syntaxe :
```lua
screens.<nom_ecran>.surface
```
Donne accès à la surface UI de l’écran, permettant de créer des éléments graphiques.
Par exemple :
```lua
local title = screens.main.surface:element({})
```
# Récupération de l'heure du jeux et du jour
```lua
TIME = "day " .. util.days_past()-1 .. " | " .. util.clock_time("HH:MM")
print(TIME .. " : " .. "Programme initialise")
```
## explication du script
- Dans un premier temps nous récupéron le jour actuelle depuis la création du monde avec : **util.days_past()** puis j'y fait -1 parceque visiblement en bas a droite dans le jeux on a un jour en moin par rapport a la function.<br/>
- Dans un second temps nous récuppérond l'heure et les minute de la journée avec : **util.clock_time("HH:MM")**, puis nous concatenons tous cela dans **TIME** avec les **..**

# Créer une interface sur laquelle placer des élément :
## Définir l'interface :
```lua
local interface = ss.ui.surface("main")
```
## Activer cette interface
```lua
ss.ui.activate("main")
```

# Créer un élement :
```lua
local panel = ui:element({
    id = "panel",
    type = "panel",
    rect = { unit = "px", x = 10, y = 10, w = 200, h = 100 },
    style = { bg = "#1E293B" },
})
```
Pour une actualisation ou un rajout d'info sans tout réecrire on peu faire :
```lua
panel:set_style({ bg = "#334155" })
panel:set_props({ text = "Updated" })
```
## suppresion d'element
```lua
ui:remove("panel")  -- Also unregisters event handlers
```
## Création d'un parent
Un exemple simple un label dans un cadre coloré :
```lua
local header = ui:element({
    id = "header",
    type = "panel",
    rect = { unit = "px", x = 0, y = 0, w = 480, h = 60 },
    style = { bg = "#111827" }
})

header:element({
    id = "title",
    type = "label",
    rect = { unit = "px", x = 20, y = 10, w = 300, h = 40 },
    props = { text = "STATUS" },
    style = { color = "#FFFFFF", font_size = 20 }
})
-- Creates element with id "header/title"
```
Syntaxe :
```lua
parent:element()
```

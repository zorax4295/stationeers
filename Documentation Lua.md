# Variable :
    Les variable en lua doivent être déclarer exemple :
        a=0
    Par défaut les varibale son déclarer global pour les déclarer local il faut le précisé exemple :
        local a=0
    les variable doivent d'abord être déclarer avant d'être utiliser. un exemple de config mauvaise :
        b = a
        local a = 0  -- ❌ b est nil ici
    Liste des déclaration possible :
        a = nil     --Absence de valeur. Par défaut si pas initialisée
        a = 1       --Entiers
        a = 3.14    --flottants
        a = "hello" --boolean
        a = true    --boolean
        a = {1,2,3} --table

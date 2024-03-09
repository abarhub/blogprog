+++
title = "gestion des shadow copy (vss) sous windows"
date = "2023-05-19"
description = "gestion des shadow copy (vss) sous windows"
tags = ["VSS","Volume Shadow Copy Service","windows"]
summary = "gestion des shadow copy (vss) sous windows"
+++
Toutes les commandes doivent être executé en administrateur.

# Liste

Pour lister les shadow copy :
`vssadmin list shadows`
```shell
vssadmin 1.1 - Outil ligne de commande d’administration du service de cliché instantané de volume
(C) Copyright 2001-2013 Microsoft Corp.

Contenu du jeu de clichés instantanés n° : {s2acebd3-14e3-4786-a53e-5ae3c8c62eba}
   Contenait 1 clichés instantanés à la date de création : 19/05/2023 18:58:50
      ID du cliché instantané : {81c4df18-1af6-1b8c-b29d-04e981ed970c}
         Volume original : (D:)\\?\Volume{c6cccf4b-dd16-4240-8bbd-5fbf9c080b2e}\
         Volume de cliché instantané : \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy41
         Ordinateur d’origine : SERVER
         Ordinateur de service : SERVER
         Fournisseur : 'Microsoft Software Shadow Copy provider 1.0'
         Type : ClientAccessible
         Attributs : Persistent, Accessible par client, Pas de libération automatique, Aucun rédacteur, Différentielle
```

# Creer

`powershell.exe -Command "(gwmi -list win32_shadowcopy).Create('E:\','ClientAccessible')"`
```shell
__GENUS          : 2
__CLASS          : __PARAMETERS
__SUPERCLASS     :
__DYNASTY        : __PARAMETERS
__RELPATH        :
__PROPERTY_COUNT : 2
__DERIVATION     : {}
__SERVER         :
__NAMESPACE      :
__PATH           :
ReturnValue      : 0
ShadowID         : {42A5CD56-3DCA-C57A-C38C-04E981ED970C}
PSComputerName   :
```

# Supprimer
Pour supprimer, la commande est :
`vssadmin delete shadows /for=C:`
```shell
vssadmin 1.1 - Outil ligne de commande d’administration du service de cliché instantané de volume
(C) Copyright 2001-2013 Microsoft Corp.

Voulez-vous vraiment supprimer 1 clichés instantanés (O/N) : [N] ? o

1 clichés instantanés ont été supprimés.
```
Il est aussi possible de supprimer en indiquer l'ID du cliché :
`vssadmin delete shadows /Shadow=c6cccf4b-dd16-4240-8bbd-5fbf9c080b2e`

# Lien

https://stackoverflow.com/a/14213304/6577778

                    
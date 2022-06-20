# Table of Contents
1. [Voyado](#voyado)
    1. [Update this](#update-this)
1. [Rule](#rule)
    1. [Configuration](#configuration)
    1. [API Keys](#api-keys)
        1. [Recommendations](#recommendations)
        1. [Data sync](#data-sync)
        1. [CLI](#cli)
        1. [Admin](#admin)
    1. [Update this](#update-this)
1. [Facebook](#facebook)
    1. [Kund](#kund)
    1. [Infobaleen](#infobaleen)
        1. [1. Lägg till kunds annonskonto](#1-lägg-till-kunds-annonskonto)
        1. [2. Lägg till FB-integrationen i plattformen](#2-lägg-till-fb-integrationen-i-plattformen)
        1. [3. Testa att integrationen är lyckad](#3-testa-att-integrationen-är-lyckad)
[](#table-of-contents)

---

[*Back to top*](#table-of-contents)

# Voyado
The voyado config needs three parameters that are the same for all lakes. These can be found on Bitwarden under Infobaleen/Voyado. The fourth parameter is the lake endpoint. This is found in Voyado's [Azure data lake]((#find-voyado-files-to-import))

Example:

```
{"Root":"/voyado/export", "Directories": ['receipts'], "ClientId": "${CLIENT_ID}", "ClientSecret": "${CLIENT_SECRET}", "DirectoryId": "${DIRECTORY_ID}", "LakeUri":"bangerhadcorestordlsprod.azuredatalakestore.net"}
```

Some comments:
* `"Directories"`: These are the directories that can be found in the [Azure data lake]((#find-voyado-files-to-import))
* There are defauly directories that will be accessible without specifying them, these are `store/`, `receiptItems/`, `article/` and `allContacts/`

[*Back to top*](#table-of-contents)

## Update this

---

[*Back to top*](#table-of-contents)

# Rule

[*Back to top*](#table-of-contents)

## Configuration
*Integration with rule enables you export your **Segmentation** campaigns to rule*  

**Name:** should be set to `rule` as standard  
**Driver:** rule  
**config:** {"ApiKey":"${rule_api_key}","KeyField":"email"}  
where `"ApiKey":"${rule_api_key}"` is set in Secrets  
and "KeyField":"email" is set ????????just a name????????  
**Default User Field:** `field name` + `KeyField` wich is set to `email` in this case  
ex. if field name = email the Default user field becomes `email email`
**Name used in exports:** ${PARENT_NAME}: ${INDEX_NAME}
**Optional User Fields:** No idea.

[*Back to top*](#table-of-contents)

## API Keys
**Name:** should be set to `rule-recommendations`  

[*Back to top*](#table-of-contents)

### Recommendations
**ItemsToItems:** `Active` dont know  
**UserToItems:** `Active` dont know  
**ItemData:** `Active` dont know  
**ModelInfo:** `Inactive` dont know  
**Data Models:** [Choose your data model with the recommendations of intrest]  
**Profiles:** [Choose the recommendation profiles you want to use]  

[*Back to top*](#table-of-contents)

### Data sync
**SourceSync:** `Inactive` dont know  
**Buffers:** `Inactive` dont know  

[*Back to top*](#table-of-contents)

### CLI
**MLDump:** `Inactive` dont know  
**Db:** `Inactive` dont know  

[*Back to top*](#table-of-contents)

### Admin
**Note:** ?????  
**Immutable:** An immutable key can never be updated (only removed). Useful if you want to share a key an be sure that the scope does not change by mistake  
**AllowAll:** Activates everything? or just recomendations tags?

 

[*Back to top*](#table-of-contents)

## Update this

---

[*Back to top*](#table-of-contents)

# Facebook

Denna integrering möjliggör uppladdning av segment som custom audiences i Facebooks Ads. 

Kräver användare med admin access till Infobaleens facebook-konto.

[*Back to top*](#table-of-contents)

## Kund
* Kund lägger till oss som partner för sitt annons konto.
    * Be dem gå till fliken Annonskonto i Business Manager och klicka tilldela partner.
    * Lägg till Infobaleens business-id 147664085678726 och välj en roll (Full control).

[*Back to top*](#table-of-contents)

## Infobaleen

[*Back to top*](#table-of-contents)

### 1. Lägg till kunds annonskonto
* När vi har fått access till annonskonto, lägg till kunds annonskonto som tillgång för vår användare _**“Sysadmin”**_ via https://business.facebook.com/settings/system-users, se bilder nedan. Klicka på knappen `Add Assets`/`Lägg till resurser` och välj `Ad Accounts`/`Annonskonton`. Välj kundens annonskonto och tilldela Full control.

<img width="1277" alt="Screenshot 2022-05-31 at 10 23 44" src="https://user-images.githubusercontent.com/4352260/171128213-3adacf8c-c680-433d-aa63-659c954e1477.png">
<img width="1160" alt="Screenshot 2022-05-31 at 10 24 45" src="https://user-images.githubusercontent.com/4352260/171128231-3a1e5d93-a8e7-4b0f-bb9b-829a49f53d35.png">

[*Back to top*](#table-of-contents)

### 2. Lägg till FB-integrationen i plattformen

Gå till kundens plattform, välj `Admin -> Configuration` och lägg in en Integration med namn `facebook-[KUNDNAMN]` och driver `facebook` (finns ej i gamla versioner av plattformen) med exempel-config enligt nedan. För field `Name used in exports` kan man specificera `${PARENT_NAME}: ${INDEX_NAME}`. 
```
{"Token":"${fb-token}", "AppSecret":"${fb-app-secret}", "AdAccountId":"act_${fb-adaccount}", "KeyField":"email", "Description":"Generated by Infobaleen."}
```

<img width="814" alt="Screenshot 2022-06-01 at 10 11 19" src="https://user-images.githubusercontent.com/4352260/171358579-48dc48f4-bca3-4f47-a55b-0c67f2722b46.png">

* **Token:** Genereras för en användare i Facebook, i det här fallet för vår systemanvändare “Sysadmin”. Finns i Bitwarden under `Collection = Infobaleen` och objektet `Facebook`.
* **AppSecret:** Genereras från vår Facebook app. Finns i Bitwarden enligt tidigare beskrivning.
* **AdAccountId:** Kundens adaccount-id. Notera att den måste ha prefix `act_` enligt exempel-config ovan. Se bild nedan för var du hittar id.
    
<img width="1117" alt="Screenshot 2022-05-31 at 12 12 59" src="https://user-images.githubusercontent.com/4352260/171150944-8e4460c8-6703-4b2b-b89a-c3de3b834c47.png">

* **KeyField:** Ange det fält på användare som innehåller email-adress.
* **Description:** Beskrivning som syns på segmentet i Facebook Ad Manager.

[*Back to top*](#table-of-contents)

### 3. Testa att integrationen är lyckad
Det vi kan se från vår sida är att uppladdningen går igenom, dels via meddelande i plattformen och sen loggar i proxyn. Bästa sättet är nog att be kunden kontrollera att det skapats ett audience i deras FB-konto.

[*Back to top*](#table-of-contents)

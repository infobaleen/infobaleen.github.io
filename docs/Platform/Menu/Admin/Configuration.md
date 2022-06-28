# Voyado
The voyado config needs three parameters that are the same for all lakes. These can be found on Bitwarden under Infobaleen/Voyado. The fourth parameter is the lake endpoint. This is found in Voyado's [Azure data lake]((#find-voyado-files-to-import))

Example:

```
{"Root":"/voyado/export", "Directories": ['receipts'], "ClientId": "${CLIENT_ID}", "ClientSecret": "${CLIENT_SECRET}", "DirectoryId": "${DIRECTORY_ID}", "LakeUri":"bangerhadcorestordlsprod.azuredatalakestore.net"}
```

Some comments:
* `"Directories"`: These are the directories that can be found in the [Azure data lake]((#find-voyado-files-to-import))
* There are defauly directories that will be accessible without specifying them, these are `store/`, `receiptItems/`, `article/` and `allContacts/`



## Update this

---



# Rule



## Configuration
*Integration with rule enables you export your **Segmentation** campaigns to rule*  

**Name:** should be set to `rule` as standard  
**Driver:** rule  
**config:** {"ApiKey":"${rule_api_key}","KeyField":"email"}  
where `"ApiKey":"${rule_api_key}"` is set in Secrets  
and "KeyField":"email" is set 
**Default User Field:** `field name` + `KeyField` wich is set to `email` in this case  
ex. if field name = email the Default user field becomes `email email`
**Name used in exports:** ${PARENT_NAME}: ${INDEX_NAME}
**Optional User Fields:** No idea.



## API Keys
**Name:** should be set to `rule-recommendations`  



### Recommendations
**ItemsToItems:** `Active` dont know  
**UserToItems:** `Active` dont know  
**ItemData:** `Active` dont know  
**ModelInfo:** `Inactive` dont know  
**Data Models:** [Choose your data model with the recommendations of intrest]  
**Profiles:** [Choose the recommendation profiles you want to use]  



### Data sync
**SourceSync:** `Inactive` dont know  
**Buffers:** `Inactive` dont know  



### CLI
**MLDump:** `Inactive` dont know  
**Db:** `Inactive` dont know  



### Admin
**Note:** 
**Immutable:** An immutable key can never be updated (only removed). Useful if you want to share a key an be sure that the scope does not change by mistake  
**AllowAll:** Activates everything or just recomendations tags


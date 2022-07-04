# Configuration

In the configuration page you can add connections to data, for example databases, and you can also add connections to integrations that you want to export data to, for example an email service.

## Databases

A database configuration is set up to fetch data into the platform, and it can be a connection to something like a data lake or a mysql server. It can look something like in the image below. Note that a parameter like `${db-user}` needs to be added in the `Secrets` page.

<img width="976" alt="Screenshot 2022-07-01 at 11 28 48" src="https://user-images.githubusercontent.com/4352260/176867875-be6a64af-1a67-48d9-88f5-689d763718d7.png">

## Integrations

An integration configuration is set up to export data from the platform.  It can look something like the facebook-export in the image below (emails are exported to Facebook). Note that a parameter like `${fb-token}` needs to be added in the `Secrets` page.

<img width="837" alt="Screenshot 2022-07-01 at 11 34 13" src="https://user-images.githubusercontent.com/4352260/176868658-b99b6f52-8a53-48f6-8e9e-b42275d10329.png">


# Partner configuration


## Voyado
The voyado config needs three parameters that are the same for all lakes. These can be found on Bitwarden under Infobaleen/Voyado. The fourth parameter is the lake endpoint. This is found in Voyado's [Azure data lake]((#find-voyado-files-to-import))

Example:

```
{"Root":"/voyado/export", "Directories": ['receipts'], "ClientId": "${CLIENT_ID}", "ClientSecret": "${CLIENT_SECRET}", "DirectoryId": "${DIRECTORY_ID}", "LakeUri":"bangerhadcorestordlsprod.azuredatalakestore.net"}
```

Some comments:
* `"Directories"`: These are the directories that can be found in the [Azure data lake]((#find-voyado-files-to-import))
* There are defauly directories that will be accessible without specifying them, these are `store/`, `receiptItems/`, `article/` and `allContacts/`


## Rule

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


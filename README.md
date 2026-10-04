# SwiftShip Tracker — Salesforce metadata export

This Salesforce DX project contains a full metadata export from the org authorized locally as `SwiftShipOrg` on 2026-10-04. The source tree has 1,026 files (approximately 6.5 MB), retrieved using the Salesforce CLI and Metadata API.

## Export scope

Every metadata type supported by both the org and the installed Salesforce CLI source registry was retrieved successfully. The export includes the SwiftShip Tracker application and its objects, flows, layouts, tabs, permissions, Prompt Builder template, Agentforce bot/planner bundle/actions, reports, profiles, settings, sharing rules, translations, standard-value-set translations, and other org configuration that the Metadata API returned.

The SwiftShip-specific retrieval manifest remains at `manifest/package.xml`.

## CLI-limited types

The org advertises the following 14 additional Metadata API types, but the installed CLI cannot retrieve or convert them because they have no local registry definition. They are listed in `manifest/unsupported-types.xml` for a future CLI update or another compatible Metadata API client:

`ActivationPlatformActvAttr`, `ActivationPlatformField`, `ActvPfrmDataConnectorS3`, `ActvPlatformAdncIdentifier`, `ActvPlatformFieldValue`, `ActvPlatformOAuthConnector`, `CustomObjectBinding`, `DataCleanRoomProvider`, `ExperienceContainer`, `MlModelConnection`, `MlModelSchema`, `PlatformEventMigration`, `StaticDynamicValMapping`, and `TagSet`.

## Verify and publish later

```bash
cd /home/saran/Work/SwiftShipTracker
sf org display --target-org SwiftShipOrg
find force-app/main/default -type f | wc -l

git init
git add .
git commit -m "Export Salesforce metadata"
git remote add origin https://github.com/OWNER/SwiftShipTracker.git
git branch -M main
git push -u origin main
```

The `.gitignore` excludes local authorization, logs, environment files, private keys, and dependencies. Do not commit passwords, access tokens, client secrets, or private keys.

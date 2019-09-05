[<- Retour](./README.md)

# Projet iOS

## Certificats Apple

Pour une application

### Créer le CSR avec une AC

Aller à https://developer.apple.com/account/ios/certificate/ et créer un certificat à l'aide d'une autorité de certification (CSR), voici comment le générer :
- Rendez-vous dans l'application **Trousseaux d'accès** située dans le dossier Applications/Utilitaires.
- Dans le menu du haut, cliquez sur **Assistant de Certification > Demander un certificat à une autorité de certificat**.
- Entrez le nom et l'email associé à votre compte Apple Developer. L'adresse e-mail de l'AC n'est pas requise. Sélectionnez Enregistrer sur disque et cliquez sur Continuer.
- Enregistrez ce fichier (**CertificateSigningRequest.certSigningRequest**) sur votre disque dur.

### App ID

Aller à https://developer.apple.com/account/ios/identifier/bundle et créer un nouvel AppID, en ayant bien cocher la case Explicit App ID, donner son Bundle ID (par défaut sur nativescript c'est : **org.nativescript.NomDeLApplication**), et cocher la case **push notifications** dans les App Services.

### Devices

Pour pouvoir builder l'application sur un iDevice (iPhone ou iPad) vous devez enregistrer cet appareil, pour ce faire :
- connectez un appareil à un port USB du Mac, iTunes s'ouvre, sous les boutons lecture / pause d'iTunes cliquez sur le logo de téléphone, puis cliquez sur **'Numéro de série'** jusqu'à voir l'**UDID** du téléphone, le copier.
- Aller à https://developer.apple.com/account/ios/device/ ajouter un device et coller l'UDID du iDevice, finir l'enregistrement du device.

### AuthKey

Aller à https://developer.apple.com/account/ios/authkey/ et créer une nouvelle clé, en cochant la case **Apple Push Notifications service (APNs)**, cliquer ensuite sur Continue et télécharger la clé, **la garder précieusement** elle ne pourra pas être retéléchargée.

### Privisioning profile
- Aller à https://developer.apple.com/account/ios/profile/ et créer un nouveau provisioning profile,
- Selectionner iOS App Development comme provisioning profile type, et cliquer sur Continue.
- Choisir l'AppID de l'application (toujours **org.nativescript.NomDeLApplication**).
- Selectionner le certificat avec lequel l'appID a été généré et cliquer sur Continue.
- Choisir les devices sur lesquel l'application va être testée, donner le nom du provisioning et générer le provisioning, le télécharger et double clic dessus pour l'installer.

## Créer l'application avec le Nativescript CLI
- Création de l'application NativeScript :
```
tns create NomDeLApplication --template tns-template-drawer-navigation-ng
```
- Ajouter le teamID Apple dans le fichier **App_Ressources/iOS/build.xconfig**
```
DEVELOPMENT_TEAM = VotreTeamID;
```
---
[<- Retour](./README.md)
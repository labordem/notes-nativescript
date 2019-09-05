[<- Retour](./README.md)

# Système de notification iOS/Android

## Ajout du plugin Nativescript Firebase
- Ajout du plugin Firebase :
```
tns plugin add nativescript-plugin-firebase
```
Répondre :
```
Are you using this plugin ONLY as a Push Notification client for an external (non-Firebase) Push service? (y/n):  (n) n
Are you using iOS (y/n):  (y) y
Are you using Android (y/n):  (y) y
Are you using Firestore? (y/n):  (n) n
Are you using Realtime DB? (y/n):  (n) n
Are you using Firebase Authentication (pretty likely if you use Firestore or Realtime DB)? (y/n):  (y) n
Are you using Firebase RemoteConfig? (y/n):  (n) n
Are you using Performance Monitoring? (y/n):  (n) n
Are you using Firebase Cloud Messaging? (y/n):  (n) y
Are you using In-App Messaging? (y/n):  (n) n
Are you using Firebase Crashlytics? (y/n):  (n) n
Are you using Firebase Crash Reporting? (answer "n" if you want to use Crashlytics instead) (y/n):  (n) n
Are you using Firebase Storage? (y/n):  (n) n
Are you using Firebase Cloud Functions? (y/n):  (n) n
Are you using Firebase Facebook Authentication? (y/n):  (n) n
Are you using Firebase Google Authentication? (y/n):  (n) n
Are you using AdMob? (y/n):  (n) n
Are you using Firebase Invites? (y/n):  (n) n
Are you using Firebase Dynamic Links? (y/n):  (n) n
Are you using ML Kit? (y/n):  (n) n

Do you want to save the selected configuration. Reinstalling the dependency will reuse the setup from: firebase.nativescript.json. CI will be easier. (y/n):  (y) y
```
Vous devez obtenir un fichier **firebase.nativescript.json** contenant exactement ces informations :
```
{
    "external_push_client_only": false,
    "using_ios": true,
    "using_android": true,
    "firestore": false,
    "realtimedb": false,
    "authentication": false,
    "remote_config": false,
    "performance_monitoring": false,
    "messaging": true,
    "in_app_messaging": false,
    "crashlytics": false,
    "crash_reporting": false,
    "storage": false,
    "functions": false,
    "facebook_auth": false,
    "google_auth": false,
    "admob": false,
    "invites": false,
    "dynamic_links": false,
    "ml_kit": false
}
```
- Ajouter ce code dans le **app/app.component.ts** :

ngOnInit(): void {
```
firebase.init({
    showNotifications: true,
    showNotificationsWhenInForeground: true,
        onMessageReceivedCallback: (message: Message) => {
            console.log(`Title: ${message.title}`);
            console.log(`Body: ${message.body}`);
            // if your server passed a custom property called 'foo', then do this:
            console.log(`Value of 'foo': ${message.data.foo}`);
        }
});
```
## Configuration depuis XCode
- Ouvrir **/platforms/ios/yourproject.xcworkspace**, dans le volet de gauche choisir **NomDeLApplication** ensuite selectionner l'onglet "Capabilities" et activer les Push Notifications (ON)
- l'étape précédente a créé un fichier <NomDeLApp>.entitlements dans ```pltaforms/ios/<NomDeLApp>```, copiez le dans votre dossier ```App_Resources/iOS/<NomDeLApp>.entitlements```
- Ouvrir ```/App_Resources/iOS/Info.plist``` et ajouter ceci à la fin du fichier pour permettre les notifications en arrière plan :
```
<key>UIBackgroundModes</key>
<array>
    <string>remote-notification</string>
</array>
```

## Console Firebase
- Il faut ensuite créer un projet depuis la console firebase : https://console.firebase.google.com/
- Ajouter une application iOS et Android, en donnant le AppID de l'application (par défaut : **org.nativescript.NomDeLApplication**)
- **IOS :** Mettre le **GoogleService-Info.plist** dans ```app/App_Resources/iOS/GoogleService-Info.plist```
- **Android :** Mettre le **google-services.json** dans ```app/App_Resources/Android/google-services.json```
- Passer les étape du SDK et de l'initialisation et laisser l'étape 5 (Exécutez votre application pour vérifier l'installation) ouverte
- Dans votre projet : Supprimer le dossier **platforms** (non suivis par git) s'il existe
- Buildez le projet : ```tns run ios```
- La page de création d'application de la console firebase devrait afficher : *Félicitations, Firebase a bien été ajouté à votre application.*
- Aller dans les paramètres du projet de la console firebase (roue dentée), aller ensuite dans l'onglet Cloud Messaging, et dans Configuration de l'application iOS ajouter la clé APN.
- Supprimez le dossier **platforms** (non suivis par git) s'il existe
- Buildez le projet : ```tns run ios```
---
[<- Retour](./README.md)
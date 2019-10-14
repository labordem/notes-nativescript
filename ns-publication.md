[<- Retour](./README.md)

## Publication d'une application NativeScript

### Icônes & SplashScreen

- Créer une icône format 1024x1024 (carré sans arrondis)
- Générer les assets avec le [NativeScript Sidekick](https://www.nativescript.org/nativescript-sidekick), modifier la taille des images *Default-1125h.png* et *Default-Landscape-X* dans **App_Resources/iOS/Assets.xcassets/LaunchImage.launchimage**, les mettre en 1125 × 2436 (si ce n'est pas déjà le cas)

### Icône de notification (Android 8+)

- Créer une icône carré, ou récupérer l'icône de l'étape précédente, mais avec avec un logo blanc sur fond transparent (pas de couleurs !!!) et générer les icones de notifications Android 8+ sur ce site : http://romannurik.github.io/AndroidAssetStudio/icons-notification.html#source.type=clipart&source.clipart=ac_unit&source.space.trim=1&source.space.pad=0&name=ic_stat_onesignal_default, les placer dans leurs dossiers respectifs
- Profitez en pour créer un logo 512x512 32 bit pour le PlayStore
- Dans **values/colors.xml** & **values-v21/colors.xml** mettre la couleur de votre choix (c'est la couleur de l'icône de la notification) comme suit :
```
<resources>
  <!--Other color entries may exist here-->
  <color name="my_special_red">#FF0000</color>
</resources>
```
- Dans **App_Resources/android/src/AndroidManifest.xml** mettre le lien vers l'icône crée ainsi que sa couleur comme dans cet exemple :
```
<application
  android:name="com.tns.NativeScriptApplication"
  android:allowBackup="true"
  android:icon="@drawable/icon"
  android:label="@string/app_name"
  android:theme="@style/AppTheme">
    <!-- INSERT THE FOLLOWING -->
    <meta-data android:name="com.google.firebase.messaging.default_notification_icon" android:resource="@drawable/my_notification_image" />
    <meta-data android:name="com.google.firebase.messaging.default_notification_color" android:resource="@color/my_special_red" />
    <!-- END OF INSERT -->
    <activity
      android:name="com.tns.NativeScriptActivity"
      android:label="@string/title_activity_kimera"
      android:configChanges="keyboardHidden|orientation|screenSize"
      android:theme="@style/LaunchScreenTheme">
```

### Publier sur le PlayStore

- Rédiger la fiche PlayStore avec votre compte développeur Google : https://play.google.com/apps/publish/
- lancer la création de la clé Keystore :
```
keytool -genkey -v -keystore NameOfYourKey.jks -keyalg RSA
-keysize 2048 -validity 10000 -alias NameOfYourApp
```
- répondre aux questions, le mot de passe est très important **le garder précieusement**
- Prendre le même mot de passe pour la clé et l'alias c'est plus simple
- Le fichier .pks généré est très important **le garder précieusement**
- Suivre la [Routine de développement](#routine-de-d%C3%A9veloppement) pour mettre en ligne votre nouvelle version

### Publier sur l'AppStore

- rédiger la fiche PlayStore avec votre comptre développeur Apple :
https://appstoreconnect.apple.com/
- Suivre la [Routine de développement](#routine-de-d%C3%A9veloppement) pour mettre en ligne votre nouvelle version

## Mettre en ligne une nouvelle version de son application sur les stores

### Numéros de version
- modifier **CFBundleShortVersionString** et **CFBundleVersion** dans **Info.plist** en respectant ce format :
  -  **CFBundleShortVersionString** : **M.m.p** (pour **M**ajeure, **m**ineure, **p**atch ex: 1.20.1)
  -  **CFBundleVersion** :  **M.m.p.m.b** (pour **M**ajeure, **m**ineure, **p**atch, **b**uild ex: 1.20.1.5) Le build est optionnel, je préfère mettre tout en **M.m.p**.
- modifier la version et le code de version dans **AndroidManifest.xml** en respectant ce format :
  - **android:versionCode** : 1, incrémenter de 1 à chaque build
  - **android:versionName** : exactement le même que le **CFBundleShortVersionString** de la version iOS en essayant de synchroniser les builds
- Résumé pour une première version :
  - CFBundleShortVersionString = CFBundleVersion = versionName = 1.0.0
  - VersionCode = 1
### Android

- Générer le nouvel AAB avec les paramètres suivants (en une seule ligne de commande sans sauts) :
```
tns build android --release
--key-store-path ~/chemin/vers/votreFichier.jks
--key-store-password votreMotDePasse
--key-store-alias NomDeLApplication
--key-store-alias-password votreMotDePasse
--aab
--bundle --env.uglify --env.aot --env.snapshot
```
- Aller dans votre tableau de bord Google Play console
- Créer une version et y déposer l'AAB généré par l'étape précédente dans 'NomDeLApplication/platforms/android/app/build/outputs/apk/release/app.aab'

### iOS
- builder pour générer le .xcworkspace de votre app :
```
tns build ios --release --bundle --env.uglify --env.aot
```
- Ouvrir le .xcworkspace avec XCode
- Indiquer la team de développement
- Dans le menu déroulant permettant de choisir le device utilisé choisir 'Generic iOS Device'
- Dans la barre de menu tout en haut de votre écran aller dans Product > Archive
- Le gestionnaire de version s'ouvre, publier la version sur l'AppStore
- Attendre de recevoir un email d'Apple indiquant que l'application est prête à être vérifiée
- Depuis l'AppStore connect créer une nouvelle version avec le bundle qui doit maintenant apparaître dans la liste des builds à vérifier, l'envoyer
- Vous allez recevoir un email vous indiquant que l'application est bien en état de vérification, elle sera publiée automatiquement par la suite (si vous avez laissé l'option par défaut).
- Committer
---
[<- Retour](./README.md)

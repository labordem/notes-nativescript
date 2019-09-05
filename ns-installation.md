[<- Retour](./README.md)

# Installation

## Mac

### Installer Node & CLI
- Installer **Xcode** depuis l'Appstore, le lancer une première fois pour accepter les licences...
- Installer **Homebrew** avec cette commande :
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
- Installer NodeJS avec cette commande :
```
brew install node
```
- Installer le NativeScript-CLI avec cette commandes :
```
npm i nativescript -g
```
### Installer les SDK et toutes les dépendances
```
tns doctor
```
choisir **configure for local builds**, et accepter TOUT les composants aditionnels. Une fois l'installation terminée se déconnecter de la session actuelle du Mac.

- Une fois reconnecté retaper la commande permettant de voir l'état de l'installation :
```
tns doctor
```
Cette fois tout doit être OK, mais si le CLI vous dit que **xcode is missing** taper cette commande, se déconnecter, et retester avec ```tns doctor```
```
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```

## Linux

### Prérequis & CLI
Avoir au préalable installé sur sa machine :
- Node
- Flatpak & FlatHub
```bash
sudo npm install -g nativescript
```
### Android SDK & Emulateur
Builder une application iOS sous Linux ou Windows n'est pas possible nativement, voici la procédure pour Android :
- Installer le Open JDK en suivant la procédure propre à votre distribution : https://openjdk.java.net/install/
- Installer Android Studio, la méthode Flatpak fonctionne sur toutes les distributions :
```
flatpak install flathub com.google.AndroidStudio
```
- Lancer Android Studio et choisir de ne pas importer de paramètre.
  - Dans l'onglet "SDK platforms", installer la dernière API
  - Dans l'onglet "SDK tools", installer l'émulateur et le build tool correspondant à la version de l'API de l'étape précédente (afficher les details pour voir toutes les versions)
  - Créer un device et lancer l'émulateur pour vérifier que tout fonctionne

**Après ceci taper les commandes suivantes :**
```
echo "export JAVA_HOME=$(update-alternatives --query javac | sed -n -e 's/Best: *\(.*\)\/bin\/javac/\1/p')" >> ~/.bashrc
echo "export ANDROID_HOME="$HOME/Android/Sdk" >> ~/.bashrc
echo "PATH=$PATH:$ANDROID_HOME/tools; PATH=$PATH:$ANDROID_HOME/platform-tools" >> ~/.bashrc
echo "alias android='$ANDROID_HOME/tools/android'" >> ~/.bashrc
echo "alias emulator='$ANDROID_HOME/tools/emulator'" >> ~/.bashrc
```
---
[<- Retour](./README.md)
<div align="center">

<img src="assets/logo.png" width="96" height="96" alt="Ereshkigal">

# Ereshkigal Project

**Flashage en un clic du firmware de test de sécurité Wi-Fi Ereshkigal RTL8720DN (BW16).**

Sans Arduino IDE. Sans code source. Sans ligne de commande. Juste ce dossier.

[English](README.md) · [Bahasa Indonesia](README.id.md) · [Español](README.es.md) · **Français** · [Deutsch](README.de.md) · [中文](README.zh.md)

![version](https://img.shields.io/badge/version-2.0.0-6c4cf1)
![plateforme](https://img.shields.io/badge/plateforme-Windows%2010%2F11-2fa565)
![carte](https://img.shields.io/badge/carte-RTL8720DN%20(BW16)-14161d)
![langues](https://img.shields.io/badge/langues%20UI-6-e0870b)

</div>

> [!WARNING]
> **Avis légal et de sécurité à lire avant usage.**
> Ereshkigal est un outil de **test de sécurité** Wi-Fi. Utilisez-le **uniquement** :
> - sur des réseaux et appareils **qui vous appartiennent**, ou pour lesquels vous avez une **autorisation écrite explicite** ;
> - dans un **environnement de laboratoire / de test contrôlé** que vous avez mis en place.
>
> **N'utilisez pas** cet outil contre des réseaux, appareils ou personnes que vous
> n'êtes pas autorisé à tester. Intercepter ou perturber des réseaux sans fil sans
> autorisation est **illégal dans la plupart des pays** et peut entraîner des
> **poursuites pénales**. Ce projet sert uniquement à l'éducation, la recherche,
> les CTF et les tests d'intrusion autorisés. **Vous êtes seul responsable de son
> usage.**

---

<p align="center">
  <img src="assets/screenshot-flasher.png" width="330" alt="Ereshkigal Project (Windows)">
  &nbsp;&nbsp;
  <img src="assets/screenshot-device.png" width="300" alt="Interface web de l'appareil Ereshkigal">
</p>
<p align="center"><sub>À gauche : le flasher sous Windows. À droite : le tableau de bord web intégré de l'appareil après flashage.</sub></p>

## Contenu

| Fichier | Description |
|---------|-------------|
| **`EreshkigalFlasher.exe`** | L'application de flashage (Windows, autonome). |
| **`Ereshkigal.efw`** | Le firmware, au format protégé d'Ereshkigal. |

Distribuez les deux fichiers ensemble. L'application est une petite fenêtre native
en **English, Bahasa Indonesia, Español, Français, Deutsch et 中文** changez via
le sélecteur en haut à droite.

## Prérequis

- **Windows 10 ou 11.** Utilise le **runtime WebView2** intégré (fourni avec
  Windows 11 et Windows 10 récent ; sinon installez une fois le *Microsoft Edge
  WebView2 Runtime* gratuit).
- Une carte **RTL8720DN / BW16** et un câble USB de **données**.
- Le **pilote USB-série** de la carte (souvent CH340 ou CP2102) pour qu'elle
  apparaisse comme un port `COM`.

## Tutoriel flashez en 4 étapes

1. **Branchez** la carte en USB et lancez **`EreshkigalFlasher.exe`**.
2. `Ereshkigal.efw` est déjà sélectionné. Choisissez le **port COM** de la carte
   dans la liste (appuyez sur actualiser s'il n'y est pas débranchez/rebranchez
   la carte puis actualisez ; l'entrée qui apparaît est votre carte).
3. Laissez **Vitesse** sur `1500000`.
4. Cliquez sur **Flasher le firmware**, attendez **Terminé**, puis redémarrez la
   carte.

La plupart des cartes passent seules en mode flashage. **Si le journal se bloque**,
faites la séquence de boutons **Mode téléchargement** sur la carte :

```
   ┌── 1 ──┐      ┌── 2 ──┐      ┌── 3 ──┐
   │ BOOT  │  →   │ RESET │  →   │ BOOT  │
   │maintns│      │appuyez│      │relâchz│
   └───────┘      └───────┘      └───────┘
   maintenez BOOT · appuyez RESET · relâchez BOOT
```

Le flasher relance la synchronisation automatiquement (jusqu'à 3×).

## Premier démarrage après flashage

1. L'appareil diffuse un réseau Wi-Fi **ouvert** nommé **`Ereshkigal`**.
2. Rejoignez-le et ouvrez **http://192.168.1.1/**.
3. Suivez l'**assistant de configuration** une fois définissez un nom de réseau
   et un mot de passe (8–63 caractères). L'appareil l'enregistre et redémarre.
4. Reconnectez-vous avec votre mot de passe, rouvrez **http://192.168.1.1/**, et le
   tableau de bord complet est débloqué.

## L'utiliser pour un contrôle WPA2 → WPA3

Ereshkigal illustre une faiblesse Wi-Fi réelle et courante : les réseaux en **WPA2
sans Protected Management Frames (PMF / 802.11w)** peuvent être perturbés par des
trames de **désauthentification** falsifiées  n'importe qui à proximité peut
déconnecter les clients, et cette déconnexion forcée est la première étape de la
capture du handshake et des attaques evil-twin.

Une évaluation **autorisée** typique sur votre propre réseau :

1. **Scan**  ouvrez le tableau de bord, appuyez sur *Scan*, choisissez le réseau cible.
2. **Users**  listez les appareils connectés.
3. **Attack**  lancez un test *deauth* et observez vos propres clients.
4. **Detector**  dédiez la radio à la détection des trames deauth dans l'air.

**Lire le résultat**
- Les clients **se déconnectent** → le réseau est en WPA/WPA2 sans PMF imposé et
  vulnérable à la falsification des trames de gestion (déni de service par deauth,
  puis l'enchaînement déconnexion-puis-capture).
- Les clients **restent connectés** → les trames de gestion sont protégées.

**La solution  passez à WPA3.** Basculez le réseau en **WPA3 (SAE)**, ou au
minimum **WPA2 avec PMF sur _requis_** (802.11w). WPA3 impose des trames de gestion
protégées, donc la deauth/dissociation falsifiée est ignorée. **Relancez le même
test deauth ensuite**  les clients devraient rester connectés, prouvant que la
mise à niveau a comblé la faille. Cet avant/après est le but : utilisez Ereshkigal
pour justifier et vérifier la migration WPA2 → WPA3.

> Uniquement sur un réseau qui vous appartient ou que vous êtes autorisé à tester, dans votre labo contrôlé.

## Dépannage

| Symptôme | Solution |
|----------|----------|
| **Aucun port COM** | Installez le pilote USB-série ; utilisez un câble de données (pas seulement de charge). |
| **« Failed to open COM… »** | Un autre programme occupe le port (moniteur série, autre flasher). Fermez-le. |
| **Réessaie puis échoue** | Faites la séquence Mode téléchargement pendant les essais : maintenez BOOT, appuyez RESET, relâchez BOOT. |
| **Toujours en échec** | Baissez la **Vitesse** à `921600` et reflashez. |

## À propos du format du firmware

`Ereshkigal.efw` est le firmware au format packagé propre à Ereshkigal. Le flasher
le prépare pour la carte en interne vous ne décompressez rien et aucun outil
supplémentaire n'est requis. Gardez le `.exe` et le `.efw` ensemble.

---

<div align="center">
<sub>Ereshkigal par <b>Titan Digitalsoft</b> · Flasher 2.0.0 · Tests autorisés uniquement</sub>
</div>

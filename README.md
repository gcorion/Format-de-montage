Pour changer le format de montage d'un disque sur un système Linux ou Windows, cela implique plusieurs étapes différentes selon le système d'exploitation. Voici les procédures pour les deux plateformes.

### 1. **Changer le format de montage sur Linux**

Sous Linux, il est fréquent de vouloir changer le système de fichiers ou de modifier la façon dont un disque est monté. Voici les étapes générales :

#### a) **Vérifier le système de fichiers actuel**
- Avant toute chose, il est utile de savoir quel est le système de fichiers actuellement utilisé. Vous pouvez utiliser la commande suivante :
  ```bash
  sudo lsblk -f
  ```
  Cela affichera une liste des disques et des partitions ainsi que leur format de fichier (par exemple, ext4, NTFS, etc.).

#### b) **Sauvegarde des données**
- Si vous comptez formater le disque, vous devez impérativement sauvegarder toutes les données importantes, car elles seront effacées.

#### c) **Démonter la partition actuelle**
- Avant de formater une partition, elle doit être démontée :
  ```bash
  sudo umount /dev/sdX1
  ```
  Remplacez `/dev/sdX1` par le chemin correct de votre disque/partition.

#### d) **Formater la partition**
- Pour formater une partition en un nouveau système de fichiers, vous pouvez utiliser `mkfs`. Par exemple, pour formater en ext4 :
  ```bash
  sudo mkfs.ext4 /dev/sdX1
  ```
  Pour un format NTFS :
  ```bash
  sudo mkfs.ntfs /dev/sdX1
  ```
  Ou encore FAT32 :
  ```bash
  sudo mkfs.vfat /dev/sdX1
  ```

#### e) **Monter la partition avec un nouveau point de montage**
- Après avoir formaté, vous pouvez monter la partition à un nouvel emplacement :
  ```bash
  sudo mount /dev/sdX1 /mnt/new_mount_point
  ```

#### f) **Ajouter au fichier `/etc/fstab` pour montage automatique**
- Si vous voulez que la partition se monte automatiquement au démarrage, éditez le fichier `/etc/fstab` :
  ```bash
  sudo nano /etc/fstab
  ```
  Ajoutez une ligne comme suit :
  ```
  /dev/sdX1  /mnt/new_mount_point  ext4  defaults  0  2
  ```

### 2. **Changer le format de montage sur Windows**

Sous Windows, changer le format d'un disque ou d'une partition peut se faire via l'interface graphique ou en utilisant `diskpart` en ligne de commande.

#### a) **Sauvegarder les données**
- Comme pour Linux, il est important de sauvegarder les données avant de formater un disque, car toutes les données seront effacées.

#### b) **Utilisation de l'interface graphique**
- Ouvrez **Gestion des disques** en appuyant sur `Win + X`, puis sélectionnez **Gestion des disques**.
- Faites un clic droit sur la partition ou le disque que vous voulez formater et sélectionnez **Formater**.
- Choisissez le nouveau format de fichier (NTFS, FAT32, exFAT) et cliquez sur **OK** pour valider.

#### c) **Utilisation de `diskpart` en ligne de commande**
- Ouvrez l'invite de commande en tant qu'administrateur (clic droit sur l'icône du menu Démarrer → **Invite de commandes (admin)**).
- Tapez `diskpart` pour entrer dans l'outil de gestion de disque.
- Affichez les disques disponibles :
  ```bash
  list disk
  ```
- Sélectionnez le disque à formater :
  ```bash
  select disk X
  ```
  Remplacez `X` par le numéro de votre disque.
- Affichez les partitions disponibles sur le disque :
  ```bash
  list partition
  ```
- Sélectionnez la partition à formater :
  ```bash
  select partition X
  ```
  Remplacez `X` par le numéro de la partition.
- Formatez la partition avec le nouveau système de fichiers :
  ```bash
  format fs=ntfs quick
  ```
  Vous pouvez remplacer `ntfs` par `fat32` ou `exfat` selon vos besoins.

### Remarques importantes
- **Sauvegarde** : Toujours sauvegarder les données avant de formater un disque, car cette opération efface toutes les données présentes.
- **Système de fichiers** : Choisissez un système de fichiers compatible avec vos besoins. Par exemple, NTFS est idéal pour Windows, tandis que ext4 est un choix commun sous Linux.

Si vous avez des étapes spécifiques ou un type de disque/partitions particulier à gérer, n'hésitez pas à le préciser !

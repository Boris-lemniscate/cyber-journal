# Semaine 1 - Mise en place du laboratoire

**Période** : du 2 au 11 octobre 2026
**Module** : 0 - Laboratoire et outils

[<-- Retour au journal](../README.md)

---

## Objectif de la semaine

Disposer d'un environnement d'expérimentation sûr et isolé, dans lequel il devient possible d'apprendre, de tester et de se tromper sans aucune conséquence sur le système principal.

## Ce que j'ai réalisé

- Vérification de la prise en charge de la virtualisation matérielle par mon processeur.
- Installation de la pile de virtualisation KVM / libvirt et de l'interface virt-manager sur Fedora.
- Téléchargement, extraction et importation d'une machine virtuelle Kali Linux 2026.2.
- Configuration de la machine : disposition du clavier, fuseau horaire, mot de passe, mises à jour.
- Création d'un instantané de référence, nommé `propre`.
- Création de mes comptes sur les plateformes d'entraînement (TryHackMe, Cisco Networking Academy, Cyberini, Hackropole) et de ce dépôt GitHub.

## Ce que j'ai appris

### La ligne de commande Linux

Avant d'installer quoi que ce soit, j'ai pris le temps d'acquérir les commandes essentielles, afin de comprendre ce que j'exécute.

| Domaine | Commandes |
| --- | --- |
| Navigation | `pwd`, `ls -la`, `cd` |
| Fichiers | `mkdir`, `touch`, `cp`, `mv`, `rm` |
| Lecture et recherche | `cat`, `grep`, `find`, `man` |
| Administration | `sudo`, `dnf search`, `dnf install`, `systemctl` |
| Édition | `nano`, `vim` |

### L'enchaînement des commandes

- `&&` exécute la commande suivante **seulement si** la précédente a réussi.
- `||` l'exécute **seulement si** la précédente a échoué.
- `;` l'exécute **dans tous les cas**.

### La virtualisation

- La commande `grep -E -c '(vmx|svm)' /proc/cpuinfo` permet de vérifier que le processeur prend en charge la virtualisation matérielle.
- Un **instantané** (*snapshot*) fige l'état complet d'une machine virtuelle et permet d'y revenir à tout moment. Il ne constitue toutefois pas une sauvegarde, puisqu'il réside dans le même fichier que le disque virtuel.

## Les difficultés rencontrées

Cette première semaine fut riche en incidents. Avec le recul, ce sont eux qui m'ont le plus appris.

### * Le mot de passe que je ne pouvais plus saisir

**Le problème** : après avoir changé mon mot de passe dans Kali, l'écran de verrouillage le refusait systématiquement, alors même qu'il fonctionnait avec `sudo`.
**La cause** : la disposition du clavier avait été modifiée pour ma session uniquement, tandis que l'écran de verrouillage utilisait la disposition du système, restée en QWERTY.
**La solution** : depuis l'hôte, la machine éteinte, j'ai réinitialisé le mot de passe et configuré le clavier système directement sur le disque virtuel grâce à `virt-customize`.
**La leçon** : un même système peut comporter plusieurs niveaux de configuration, et il est parfois plus simple d'intervenir depuis l'extérieur de la machine que depuis l'intérieur.

## Ce que je retiens

> L'instantané que l'on n'a pas créé est toujours celui dont on aurait eu besoin.

Ces incidents m'ont fait comprendre, par l'expérience plutôt que par la théorie, pourquoi les administrateurs systèmes accordent tant d'importance aux sauvegardes, aux points de restauration et à la prudence lors des mises à jour.


## La semaine prochaine

Début du **module 1 - Culture de la cybersécurité** : le MOOC de Cyberini.
 

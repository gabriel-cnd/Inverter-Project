# Cahier des charges – Onduleur monophasé

## 1. Objectif du projet

Concevoir, réaliser et valider un **onduleur monophasé DC/AC en pont en H**, depuis la simulation jusqu’aux essais expérimentaux.

Le projet comprend :

- la modélisation sous **PLECS** ;
- le dimensionnement des composants ;
- la conception du PCB ;
- la validation **Hardware-in-the-Loop (HIL)** ;
- l’assemblage ;
- les essais et mesures sur le convertisseur.

## 2. Spécifications principales

| Paramètre                     | Exigence                           |
| ----------------------------- | ---------------------------------- |
| Topologie                     | Pont en H monophasé                |
| Tension d’entrée              | **400 V DC**                       |
| Tension de sortie             | **230 V RMS AC**                   |
| Puissance nominale            | **1 kW**                           |
| Fréquence de commutation      | **40 kHz**                         |
| Charge de référence           | Résistive **R**                    |
| Filtre de sortie              | Inductif **L**                     |
| Ondulation du courant ΔIL,max | **≤ 30 % de IRMS nominal**         |
| THD du courant de sortie      | **≤ 2 %**                          |
| Contrôle                      | **TI F2837x, connecteur 180 pins** |
| PCB                           | **4 couches**                      |
| Budget                        | **< 100 CHF**                      |

## 3. Travaux à réaliser

Le projet doit comprendre :

- modélisation complète de l’onduleur sous **PLECS** ;
- dimensionnement du **filtre inductif** ;
- dimensionnement des **semi-conducteurs de puissance** ;
- conception des **drivers de grille** ;
- dimensionnement des **snubbers** ;
- conception de la **chaîne de mesure** ;
- conception du schéma et du PCB sous **KiCad** ;
- prise en compte des contraintes d’**isolement 800 V** ;
- prise en compte des contraintes de **compatibilité électromagnétique (CEM)** ;
- validation de la commande en **HIL** ;
- assemblage et essais progressifs du convertisseur.

## 4. Protections obligatoires

Le convertisseur devra intégrer :

- une protection **hardware contre les courts-circuits de branche** ;
- une protection contre les **surintensités en sortie** par fonction **Trip-Zone**, avec déclenchement rapide de l’ordre de **1 à 2 µs** ;
- une surveillance de la **tension du bus DC** contre les surtensions et sous-tensions ;
- une surveillance de la **température des semi-conducteurs** ;
- une **isolation galvanique** des signaux de commande et de mesure.

## 5. Sécurité

Les essais devront respecter les exigences suivantes :

- décharge du bus DC jusqu’à **60 V en moins de 10 s** après coupure ;
- utilisation de **mesures isolées** ;
- première mise sous tension à **tension réduite et courant limité** ;
- vérification préalable des signaux de grille et des **temps morts** ;
- présence d’un **arrêt d’urgence** lors des essais ;
- zone de travail sécurisée ;
- utilisation des **EPI nécessaires**.

## 6. Critères de validation

Le système doit permettre la conversion suivante :

**400 V DC → pont en H → filtre L → 230 V RMS AC / 1 kW**

Les critères principaux de validation sont :

- **THD du courant de sortie ≤ 2 %** ;
- **ΔIL ≤ 30 % de IRMS nominal** ;
- commande fonctionnelle ;
- protections fonctionnelles ;
- validation préalable en simulation ;
- validation en HIL ;
- fonctionnement expérimental du convertisseur.

La configuration minimale à valider est constituée de :

- une source DC idéale ;
- un pont en H monophasé ;
- un filtre inductif **L** ;
- une charge résistive **R**.

Les éventuelles extensions du système ne doivent être réalisées qu’après validation complète de cette configuration de base.

## 7. Livrables

À la fin du projet, les éléments suivants devront être fournis :

- **rapport final** avec les étapes de conception, calculs et mesures ;
- modèles de simulation **PLECS** ;
- modèles de simulation **HIL** ;
- dossier **KiCad complet** :
  - schémas ;
  - nomenclature ;
  - fichiers Gerber ;
  - autres fichiers nécessaires à la fabrication ;
- code source commenté pour la carte **TI F2837x**, ou projet PLECS utilisé pour la programmation ;
- **PCB assemblé et testé** ;
- rapport de mesures sur le convertisseur opérationnel.

## 8. Jalon critique

Le **PCB doit être finalisé et validé avant le 13 décembre 2026** afin de permettre le lancement de sa fabrication.

## 9. Résumé

> Concevoir et réaliser un onduleur monophasé en pont H de **1 kW**, alimenté sous **400 V DC** et fournissant **230 V RMS AC**, commandé à **40 kHz**, avec un **THD ≤ 2 %**, un filtre inductif, des protections complètes, un **PCB 4 couches** et un budget inférieur à **100 CHF**.

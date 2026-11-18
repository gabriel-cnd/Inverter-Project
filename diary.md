# Diary — Inverter Project

Journal des **décisions**, **modifications** et **points à valider**. Les modèles présents dans le dépôt ne doivent pas être confondus avec des résultats expérimentaux ou une validation HIL réalisée.

## 1. Choix de configuration

### 1.1 Configuration de référence (obligatoire)

- Source de tension **400 V DC**.
- Onduleur **monophasé en pont en H**.
- Filtre de sortie **inductif L**.
- Charge **résistive R**.
- Objectifs nominaux : **230 V RMS**, **1 kW**, **40 kHz**, **THD du courant ≤ 2 %**.

Cette configuration doit être validée avant toute extension.

### 1.2 Orientation retenue pour une extension

- **Configuration étendue : grid-tied**.
- **Réseau monophasé**.
- **Inductance de couplage au réseau**.

Ce choix est consigné dans le journal initial du 16 septembre. Il représente une **orientation de projet**, pas une fonction déjà réalisée ni une exigence remplaçant la configuration de base. Les points à justifier restent : intérêt de l'application, solutions alternatives, commande synchronisée et protections.

## 2. Journal chronologique

### 2026-09-16 — Elisa : orientation de l'application

- Choix noté dans le journal initial : **configuration étendue grid-tied**.
- Architecture envisagée : réseau monophasé avec inductance de couplage.
- **À compléter :** argumentaire comparatif et motivation du choix.

### Septembre 2026 — Première simulation PLECS

- Création du modèle `01_Inverter_OpenLoop.plecs`.
- Point de départ : étude de l'étage de puissance en **boucle ouverte**.
- **À documenter :** paramètres de simulation, formes d'onde et vérification de la tension de sortie.

### 2026-09-27 — Temps morts et compensation

- Développement de la version avec **temps morts** (`02_...`).
- Développement de la version avec **compensation des temps morts** (`03_...`).
- Objectif : comparer les effets sur la commande et la tension/courant de sortie.
- **À documenter :** valeur des temps morts, méthode de compensation et comparaison quantitative.

### 2026-09-29 — Préparation HIL

- Adaptation des trois premières simulations à une architecture **HIL / RT-BOX**.
- Résolution, pendant les essais de simulation, d'un problème lié au paramétrage des **blanking times**.
- **À vérifier séparément :** simulation offline avec le template et fonctionnement réel sur la RT-BOX.

### Octobre 2026 — Régulation en boucle fermée

- Ajout d'un modèle avec **régulateur proportionnel (P)**.
- Ajout d'un modèle avec **régulateur proportionnel-résonant (PR)**.
- Les modèles sont conservés comme étapes distinctes du développement.
- **À documenter :** schéma de retour, grandeur régulée, paramètres des régulateurs, réponse dynamique, erreur statique, THD et limites de commande. Aucune performance n'est présumée validée.

### 2026-10-18 — Organisation du dépôt GitHub

- Ajout des modèles PLECS 02 à 05 dans `simulations/plecs/`.
- Ajout des modèles HIL 01 à 03 et du template dans `simulations/HIL/`.
- Mise à jour de la documentation en préparation.
- **À confirmer :** commit et push sur `main`.

### 2026-10-27 — Premier rendu et étude électrothermique

- Finalisation du rapport du premier jalon, archivé dans `docs/rendus/01/`.
- Choix documenté du MOSFET SiC **Wolfspeed C3M0060065D** (650 V, 60 mΩ, TO-247-3).
- Ajout du modèle `HIL_04_Inverter_OpenLoop_MOSFET_Thermal.plecs` intégrant l'analyse des pertes et des températures.
- Ajout du modèle de pertes PLECS et de la fiche constructeur dans `datasheets/`.
- Les résultats du rapport restent des résultats de simulation offline tant qu'aucune preuve d'exécution sur la RT-BOX physique n'est fournie.

### 2026-11-17 — Préparation du driver, du snubber et du PCB

- Ajout du document pédagogique de dimensionnement du driver MOSFET et du snubber dans `docs/rendus/02/`.
- Ajout des guides de conception KiCad dans `hardware/kicad/`.
- Ces guides constituent des références de conception ; aucun schéma ni routage KiCad du convertisseur n'est encore présent dans le dépôt.

## 3. Sources

### Documents du projet

- [Énoncé officiel du mini-projet](Mini_Project_conception_ELPU2.pdf).
- Document « Mini-projet de conception - Rendu 1 », daté du 13 octobre 2026 (à intégrer au dépôt si souhaité).

### Source utilisée pour les choix techniques

- [Commande d'un onduleur : réseau ou isolé, monophasé](https://www.sirepe.fr/commande-dun-onduleur-reseau-ou-isole-monophase-de-3-kva/) : source déjà référencée dans le journal initial pour le schéma de commande.

## 4. Points à clarifier et résultats à produire

- [ ] Justifier l'intérêt du **grid-tied** et comparer avec la charge résistive de référence.
- [ ] Vérifier et documenter **230 V RMS**, **1 kW**, ondulation du courant et **THD ≤ 2 %**.
- [ ] Mesurer / documenter les conséquences des **temps morts** et le gain de la compensation.
- [ ] Comparer objectivement les régulateurs **P et PR** en boucle fermée.
- [x] Justifier le choix du semi-conducteur **C3M0060065D** et effectuer un premier dimensionnement de son refroidissement.
- [x] Effectuer et documenter une première **simulation thermique PLECS**.
- [ ] Produire des preuves de simulation **offline** avec le template HIL.
- [ ] Valider la commande en **temps réel sur RT-BOX**.
- [ ] Définir, si l'extension réseau est poursuivie, la synchronisation et les protections requises.

## 5. Prochaines étapes

1. Vérifier l'ouverture du modèle thermique portable sur une seconde installation PLECS.
2. Valider la commande en temps réel sur la RT-BOX et archiver les preuves de mesure.
3. Poursuivre le dimensionnement du driver, du snubber et des protections.
4. Créer le schéma puis le PCB quatre couches sous KiCad avant le jalon du 13 décembre 2026.

## 6. Suivi du deuxième rendu

- [ ] Rappeler le cahier des charges
- [ ] Définir l’architecture générale du pont en H
- [ ] Choisir le driver de grille isolé
- [ ] Calculer le courant de grille
- [ ] Dimensionner les résistances de grille
- [ ] Dimensionner les alimentations isolées des drivers
- [ ] Définir le temps mort
- [ ] Concevoir les protections
- [ ] Dimensionner les snubbers RC
- [ ] Sélectionner les composants commerciaux
- [ ] Établir la nomenclature et vérifier le budget
- [ ] Réaliser le schéma électrique sous KiCad
- [ ] Vérifier le schéma avec l’ERC
- [ ] Implanter et router le PCB quatre couches
- [ ] Vérifier l’isolation, les boucles de commutation et la CEM
- [ ] Valider la conception par simulation et mesures
- [ ] Rédiger le rapport de dimensionnement

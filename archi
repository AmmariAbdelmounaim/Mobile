# Cahier des charges - Detection des routines conducteur

## 1. Contexte

Dans le cadre du developpement de vehicules electriques connectes, Ampere souhaite etudier la faisabilite d'une application Android embarquee capable de detecter les habitudes du conducteur sur plusieurs reglages vehicule, puis de proposer des automatisations de routines pertinentes.

Le projet cible principalement les usages suivants :

- climatisation
- mode de conduite
- infotainment
- correlation avec le contexte d'usage : lieu, destination, temps, profil conducteur

L'objectif n'est pas uniquement de produire un algorithme, mais un prototype techniquement credible pour une future integration produit.

## 2. Vision du projet

Le systeme doit apprendre les routines personnelles d'un conducteur a partir des interactions observees, puis proposer au bon moment des suggestions discretes du type :

"Vous activez souvent le mode Eco et la climatisation a 21 degres lorsque vous partez au travail le matin. Voulez-vous appliquer cette routine ?"

La solution doit etre :

- explicable
- modulaire
- compatible embarque
- respectueuse de la vie privee
- evaluable objectivement

## 3. Objectifs

### 3.1 Objectif principal

Concevoir, developper et demontrer une application Android capable de detecter des routines conducteur en temps quasi reel et de proposer une automatisation avec confirmation utilisateur.

### 3.2 Objectifs secondaires

- construire une base de donnees exploitable a partir de logs reels et augmentes
- definir un pipeline de traitement et d'apprentissage hors ligne
- integrer un moteur d'inference embarque dans une application Android
- produire une documentation technique orientee integration produit
- preparer une evolution vers des recommandations par conducteurs similaires

## 4. Perimetre fonctionnel

### 4.1 Perimetre du MVP

Le MVP couvre prioritairement les routines de depart de trajet recurrent, notamment :

- domicile vers travail
- travail vers domicile

Fenetre fonctionnelle couverte :

- avant depart
- debut de trajet

Types de recommandations pris en charge :

- climatisation : activation, mode auto, temperature cible discretisee
- mode de conduite : Eco, Normal, Sport
- infotainment : source favorite ou preset simple

### 4.2 Hors perimetre du MVP

- apprentissage continu complet directement sur le vehicule
- automatisation sans validation utilisateur
- couverture exhaustive de tous les reglages vehicule
- optimisation par backend distant obligatoire
- moteur collaboratif complet entre conducteurs similaires
- modeles profonds opaques comme coeur du MVP

## 5. Utilisateurs cibles

### 5.1 Utilisateur final

Le conducteur d'un vehicule electrique utilisant des profils differencies et des habitudes recurrentes.

### 5.2 Utilisateurs internes du projet

- encadrants techniques Android/embarque
- equipe IA/data
- equipe produit/UX
- equipe integration vehicule

## 6. Hypotheses structurantes

Les hypotheses retenues pour ce projet sont les suivantes :

- livrable vise : prototype produit credible
- entrainement des routines hors ligne
- inference on-device dans l'application Android
- recommandations avec confirmation utilisateur
- apprentissage hybride avec priorite au profil conducteur
- routine definie comme un pack d'actions correlees dans un contexte donne
- routines personnelles en v1
- filtrage par conducteurs similaires en v2
- declenchement evenementiel
- moteur explicable en deux etages : contexte puis scoring
- lieux representes par zones significatives
- temps represente de facon semantique et discretisee
- trois moteurs de domaine : clim, mode de conduite, infotainment
- fusion partielle des recommandations selon les niveaux de confiance
- abstention automatique en dessous d'un seuil de confiance
- privacy by design forte

## 7. Cas d'usage prioritaires

### 7.1 Cas d'usage principal

En debut de journee, lorsqu'un conducteur charge son profil et prepare un trajet domicile vers travail, le systeme detecte une routine recurrente et propose un pack d'actions adapte.

### 7.2 Cas d'usage secondaires

- trajet retour travail vers domicile
- suggestion partielle si un seul domaine est fortement confiant
- absence de suggestion si le contexte est incertain
- journalisation des reponses utilisateur pour amelioration future

## 8. Exigences fonctionnelles

### 8.1 Collecte et observation

Le systeme doit pouvoir observer et journaliser au minimum :

- timestamp des evenements
- profil conducteur
- zone significative d'origine
- destination ou cluster de destination
- etat de climatisation
- mode de conduite
- etat infotainment cible
- evenements de demarrage, debut de trajet, arret
- feedback utilisateur sur les suggestions

### 8.2 Construction du contexte

Le systeme doit transformer les donnees brutes en contexte metier interpretable incluant :

- conducteur
- moment de la journee
- type de jour
- zone d'origine
- destination semantique
- phase du trajet

### 8.3 Detection et recommandation

Le systeme doit :

- detecter les routines compatibles avec le contexte courant
- calculer un score de confiance par domaine
- fusionner les domaines suffisamment confiants
- proposer une suggestion discrete a l'utilisateur
- appliquer les reglages uniquement apres confirmation
- s'abstenir si le score est inferieur au seuil

### 8.4 Feedback et evaluation

Le systeme doit conserver :

- acceptation
- refus
- absence de reponse
- action effectivement realisee ensuite par le conducteur

## 9. Exigences non fonctionnelles

### 9.1 Performance

- latence cible de recommandation inferieure a 1 seconde apres evenement declencheur
- fonctionnement sans connexion reseau obligatoire
- impact limite sur les ressources du terminal embarque

### 9.2 Securite et vie privee

- stockage local par defaut
- export de donnees pseudonymise
- separation entre logs bruts, features et routines derivees
- retention maitrisee des donnees
- pas d'exposition du GPS brut dans le moteur metier

### 9.3 Qualite logicielle

- modularite forte entre UI, acces donnees, moteur de routines et journalisation
- testabilite du moteur sans dependance a l'interface Android
- versionnement des artefacts embarques
- tracabilite des decisions et du feedback

### 9.4 Explicabilite

Chaque recommandation doit pouvoir etre justifiee de facon simple, par exemple :

- contexte detecte
- raison principale de la suggestion
- niveau de confiance

## 10. Donnees du projet

### 10.1 Sources de donnees

Le projet s'appuie sur un mix de donnees :

- captures reelles sur vehicule ou environnement simule
- rejeu de scenarios representatifs
- augmentation controlee pour enrichir les patterns

### 10.2 Principes de modelisation

- zones significatives plutot que coordonnees brutes
- destinations regroupees en clusters ou labels semantiques
- temps discretise par plages et types de jour
- actions ciblees discretisees pour limiter la sparsity

## 11. Approche algorithmique retenue

### 11.1 MVP

Le MVP repose sur un moteur hybride explicable :

1. construction du contexte
2. recherche de routines candidates
3. scoring a partir de frequence, recence, stabilite et co-occurrence
4. fusion partielle par domaine
5. application d'une policy de confiance et de cooldown

### 11.2 Evolutions possibles

- calibration automatique plus fine des seuils
- reranking par modele leger
- recommandation collaborative basee sur profils similaires
- adaptation saisonniere plus poussee

## 12. Architecture de reference

Le systeme est compose de deux blocs principaux :

- pipeline offline en Python pour l'analyse, l'evaluation et la generation d'un snapshot versionne
- application Android en Kotlin pour l'inference temps reel et l'interaction utilisateur

Le moteur embarque s'appuie sur :

- une couche d'acces aux signaux vehicule ou mockes
- une couche de journalisation locale
- un constructeur de contexte
- trois moteurs metier par domaine
- une couche de fusion
- une policy d'affichage et de decision

Le detail de l'architecture est documente dans le fichier `architecture-projet-routines-conducteur.md`.

## 13. Livrables attendus

Les livrables minimaux du stage sont :

- application Android prototype demonstrateur
- simulateur ou adaptateur mock des signaux vehicule
- pipeline Python d'exploitation des logs et de generation de snapshot
- jeu de donnees de travail documente
- evaluation du MVP sur logs rejoues
- documentation technique d'architecture et d'integration produit
- rapport de stage / support de soutenance

## 14. Criteres d'acceptation du projet

Le projet sera considere comme reussi si les conditions suivantes sont remplies :

- une application Android fonctionnelle presente des suggestions de routines en contexte
- le moteur tourne en local avec un artefact embarque versionne
- les recommandations sont explicables
- la demo fonctionne a partir de logs ou evenements simules et/ou reels
- les metriques principales sont produites et analysees
- la documentation permet d'envisager une industrialisation ulterieure

## 15. Metriques de succes

### 15.1 Metriques principales

- acceptance rate
- false positive rate
- latence de recommandation

### 15.2 Metriques secondaires

- couverture des situations ou une suggestion est emise
- taux d'abstention
- stabilite des recommandations selon le profil et le contexte

## 16. Contraintes et risques

### 16.1 Contraintes

- acces potentiellement limite au vehicule reel
- disponibilite incertaine de certains signaux systeme
- volume initial de donnees potentiellement faible
- contraintes privacy et embarque fortes

### 16.2 Risques projet

- bruit ou manque de qualite des donnees
- cold start trop penalise pour les premiers usages
- UX intrusive si les seuils sont mal calibres
- surcomplexification algorithmique pour un gain faible

### 16.3 Reponses prevues

- simulateur et rejeu de scenarios
- strategie cold start a trois niveaux
- moteur explicable plutot qu'opaque
- policy stricte d'abstention et de cooldown

## 17. Strategie de validation

La validation du projet repose sur deux approches complementaires :

1. evaluation offline sur logs rejoues
2. demonstration live sur application Android avec evenements mockes ou reels

Cette strategie permet de demontrer a la fois :

- la qualite des recommandations
- la faisabilite temps reel
- la credibilite d'une integration embarquee

## 18. Macro planning propose

### Phase 1 - Cadrage et instrumentation

- cadrage des signaux disponibles
- definition du modele de donnees
- mise en place de la journalisation et du simulateur

### Phase 2 - Pipeline data et detection de routines

- transformation des donnees
- construction des features
- premier moteur de scoring explicable

### Phase 3 - Integration Android

- chargement du snapshot
- inference embarquee
- affichage des suggestions
- collecte du feedback

### Phase 4 - Evaluation et calibration

- bench offline
- calibration des seuils
- ajustement de la policy d'affichage

### Phase 5 - Finalisation

- documentation technique
- scenario de demo
- perspectives v2

## 19. Perspectives d'evolution

Les evolutions envisagees apres le MVP sont :

- filtrage collaboratif par conducteurs similaires
- prise en compte de saisons et conditions exterieures
- enrichissement des domaines de reglages
- apprentissage personnalise plus frequent
- integration plus profonde aux services vehicule embarques

## 20. Conclusion

Ce projet vise a demontrer qu'un moteur de detection de routines conducteur peut etre concu de facon industrialisable, explicable et compatible embarque. Le MVP priorise la valeur produit, la sobriete technique et la tracabilite, tout en laissant une voie claire vers des recommandations plus avancees a moyen terme.

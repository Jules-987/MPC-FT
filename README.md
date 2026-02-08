Cahier des charges — Refonte d’apparence Fluent Design

Projet : MPC-FT (Fluent Theme Pack)
Base : MPC-BE / MPC-HC (fork interne “MPC BE”)
Version : V1 — “Look & Feel only”
Auteur : Jules
Date : 08/02/2026

1) Contexte et justification

Le logiciel actuel (MPC BE / HC) fonctionne, mais son interface est perçue comme datée.
Le projet vise une refonte esthétique inspirée de Fluent Design (Windows 10/11) afin d’améliorer :

la lisibilité

la cohérence visuelle

la modernité perçue

la qualité “produit” (finition UI)

Sans toucher à la logique métier ni aux capacités de lecture.

2) Objectif principal

Créer une variante visuelle nommée MPC-FT apportant une esthétique Fluent :

plus épurée

plus cohérente

plus “Windows 11-ready”

sans modification de l’agencement (layout) ni des fonctionnalités

3) Périmètre fonctionnel
Inclus (dans la V1)

Thème visuel global : couleurs, contrastes, typographies, espacements perçus, styles des contrôles

Barre de titre + chrome fenêtre (dans la limite des possibilités MFC/Win32)

Barre d’outils (toolbar) : icônes, fonds, états hover/pressed/disabled

Menus (menu bar + context menus) : couleur, survol, séparateurs

Boîtes de dialogue existantes : préférences, “À propos”, etc. (re-skin)

Contrôles UI : boutons, checkbox, radio, sliders, listviews, treeviews, tab controls

Mode clair + mode sombre

Identité : nom fenêtre “MPC-FT – Entreprise”, logo, icône app (si possible)

Exclus (hors V1)

Aucune nouvelle feature (playlist, codecs, pipeline, lecture, etc.)

Aucune refonte d’agencement (pas de nouveaux panneaux, pas de repositionnement majeur)

Pas de migration de framework (pas de WPF/WinUI)

Pas de changement de comportement (raccourcis, lecture, filtres, etc.)

4) Exigences UI/UX (Fluent)
4.1 Principes visuels

Hiérarchie nette : fond calme, actions visibles

Contraste maîtrisé : lisible en plein écran et en faible luminosité

Densité réduite : l’interface respire, sans bouger les éléments

États interactifs clairs : hover/pressed/focus/disabled

4.2 Styles requis

Coins arrondis (léger) : là où c’est faisable sans casser MFC

Ombres discrètes : uniquement si stable et sans artefacts

Effets “material” : optionnel (Mica/Acrylic), activable si compatible

V1 : ce sera “best effort”, avec fallback propre.

4.3 Typographie

Police système Windows (Segoe UI / variable selon OS)

Tailles inchangées si possible, mais meilleure lisibilité via couleurs/contrastes

5) Exigences techniques
5.1 Stack et build

Langage : C++ (MFC/Win32)

IDE : Visual Studio (version récente)

Toolset : v143 (obligatoire pour MFC disponible)

Windows SDK : 10 ou 11

Compilation cible : x64 (priorité), Win32 optionnel

5.2 Contraintes

Ne pas casser la compatibilité Windows cible actuelle du projet (à définir : Win10 min recommandé)

Performance UI : aucun ralentissement perceptible (menus/toolbar/dialogs)

Fallback : si un effet (Mica/Acrylic) n’est pas dispo, le rendu doit rester propre

6) Architecture du thème
6.1 Organisation attendue

Un “theme layer” central (ex : CMPCTheme*) qui :

fournit palette couleurs

gère dark/light

dessine les contrôles (owner-draw si nécessaire)

Ressources séparées :

icônes (SVG/PNG/ICO selon contraintes existantes)

bitmaps toolbar

couleurs/thèmes centralisés

6.2 Nommage

App : MPC-FT

Titre fenêtre : MPC-FT – Entreprise

Variante V1 : MPC-FT (Fluent Theme Pack)
(tu peux aussi appeler ça “MPC-FT Nova”, “MPC-FT Prism”, “MPC-FT Aurora” — on tranchera plus tard)

7) Livrables
Livrables V1 (obligatoires)

Une build fonctionnelle de MPC-FT (x64)

Thème clair + sombre cohérents

Ressources graphiques (icônes/toolbar) versionnées

Guide interne court :

comment compiler

où changer la palette

où sont les ressources

Livrables V1 (souhaitables)

Page “À propos” mise à jour (nom + logo)

Capture d’écran “avant/après” (même fenêtre)

8) Critères d’acceptation (tests de validation)

Le livrable est accepté si :

L’application compile et se lance

Aucun changement fonctionnel observable

Menus/toolbar/dialogs ont un style Fluent homogène

Dark mode lisible (contraste OK)

Pas de glitch évident (clignotement, artefacts de redraw)

Aucun crash introduit

9) Risques et parades

MFC limite certains effets → parades : fallback, owner-draw ciblé

Thème dispersé dans le code → parade : centraliser palette + styles

Dépendances build lourdes (ffmpeg/mingw) → parade : workflow “UI build minimal” au début

10) Plan de réalisation (séquencé)
Phase 0 — Build stable

Toolset v143 + SDK 10/11

Submodules OK

Lancement mpc-hc64.exe

Phase 1 — Palette + Dark/Light

définir 8–12 couleurs maîtres

appliquer aux surfaces principales

Phase 2 — Toolbar + Menus

icônes modernisées

hover/pressed/focus cohérents

Phase 3 — Dialogs (Préférences, etc.)

harmoniser contrôles

spacing visuel sans bouger les layouts

Phase 4 — Finitions

titre fenêtre, branding, icône

polish (focus rings, separators, scrollbar)

# DESIGN.md · Outil Causal Impact (version publique)

Règles visuelles et d'interface de `index.html`. Toute évolution les suit ; un besoin nouveau (une couleur, un espacement, un composant) s'ajoute ici une fois, puis s'utilise par son nom. Le moteur `ci-engine.js` n'est pas concerné.

## 1. Intention
* **Ton** : instrument clinique et technique pour analystes. Pas de décoration.
* **Image** : un classeur de protocole de laboratoire. Des étapes numérotées, chacune validée avant la suivante.
* **Figure centrale** : le graphique observé contre contrefactuel (courbe observée, prédiction en tirets, bande d'intervalle). Tout le reste sert à y arriver proprement.
* **Principe de lecture** : l'outil montre la confiance et l'intervalle sans trancher. La grille 95 / 90 / 70 est une légende, pas un verdict.

## 2. Couleurs
Thème sombre unique (`color-scheme: dark`), fond noir intégral. Aucune couleur hors de cette liste.

| Variable | Valeur | Usage |
|---|---|---|
| `--bg` | `#000000` | Fond de page, champs de saisie, texte des boutons primaires |
| `--panel` | `#101214` | Cartes, tuiles, boutons neutres, notifications, menus, infobulles |
| `--ink` | `#E8EAED` | Texte principal, courbe observée |
| `--muted` | `#9AA1AA` | Texte secondaire, libellés, en-têtes de tableau |
| `--line` | `#262A2F` | Bordures, filets, séparateurs |
| `--line-hover` | `#3A4047` | Bordure d'un bouton survolé |
| `--accent` | `#7FB0E0` | Le modèle (contrefactuel), action primaire, liens, focus, étape active |
| `--accent-hover` | `#94BFE8` | Bouton primaire survolé |
| `--band` | `rgba(127,176,224,.22)` | Bande d'intervalle à 95 % |
| `--shade` | `rgba(232,234,237,.07)` | Fond de la pré-période sur les graphiques |
| `--grid` | `#1A1D21` | Grille des graphiques |
| `--flag` | `#FF6B6B` | Alertes, erreurs, « À relancer », action destructive. Jamais décoratif |
| `--ok` | `#6FCF97` | Contrôle passé, étape faite |

Règles :
* Un seul accent. Le bleu signifie « le modèle » ou « l'action à faire ».
* Le rouge signifie « attention » ou « destructif ». Le vert signifie « contrôle passé ». Ne jamais les utiliser pour orner.
* Le sens ne passe jamais par la couleur seule : une puce de couleur est toujours accompagnée d'un texte (« 2 pics isolés », « Exposée »).
* Fonds teintés autorisés : rouge à 9 % (ligne de tableau en alerte), rouge à 13 % (puce d'alerte).

Contrastes mesurés (WCAG) :

| Texte | Sur `--bg` | Sur `--panel` |
|---|---|---|
| `--ink` | 17,4:1 | 15,6:1 |
| `--muted` | 8,1:1 | 7,2:1 |
| `--accent` | 9,2:1 | 8,2:1 |
| `--flag` | 7,6:1 | 6,8:1 |
| `--ok` | 11,0:1 | 9,9:1 |

Texte noir sur `--accent` (bouton primaire) : 9,2:1.

## 3. Typographie
* **Titres** : Inter Tight 600. `h1` 20 px (nom de l'outil), `h2` 24 px (titre d'écran), `h3` 16 px (section).
* **Texte** : Inter 400 / 500 / 600, 15 px, interlignage 1,5. Repli : `system-ui, Arial, sans-serif`.
* **Petits textes** : 13 à 13,5 px (tableaux, notes), 12 à 12,5 px (en-têtes de tableau, libellés de tuiles, puces). Rien sous 12 px, sauf les graduations des graphiques (11 px).
* **Chiffres** : `font-variant-numeric: tabular-nums` dans les tableaux, tuiles et résultat principal. Colonnes numériques alignées à droite, sans retour à la ligne.
* **Résultat principal** (`.hero .big`) : Inter Tight 600, `clamp(40px, 7vw, 64px)`.
* Polices chargées depuis Google Fonts (Inter 400, 500, 600 ; Inter Tight 600).

## 4. Espacements, grilles, rayons
* **Largeur de contenu** : 1 240 px maximum ; textes d'introduction et notes limités à 760 px ; pages Mode d'emploi et Lexique à 820 px.
* **Marges latérales** : `max(3vw, 16px)`.
* **Grille de formulaire** (`.grid`) : colonnes automatiques de 230 px minimum, écarts 12 × 18 px, champs alignés en bas (un libellé sur deux lignes ne décale pas les champs voisins).
* **Tuiles** (`.tiles`) : colonnes de 170 px minimum, écart 10 px ; 2 colonnes sous 720 px.
* **Rangées de boutons** (`.row`) : écart 10 px, marge verticale 12 px.
* **Sections** (`.sec`) : filet en haut, 26 px au-dessus.
* **Rayons** : 6 px (boutons, champs, notes), 8 px (tuiles, panneaux, zone de dépôt, notifications, menus), 10 px (puces), 4 px (barres de progression et d'inclusion).
* **Hauteur minimale des contrôles** : 40 px (boutons, champs). Exceptions : boutons d'action en tableau 30 px, sélecteurs en tableau 34 px, boutons de la notification 32 px.

## 5. Composants
* **Bouton neutre** : fond `--panel`, bordure `--line` ; survol : bordure `--line-hover` ; appui : descend de 1 px.
* **Bouton primaire** (`.primary`) : fond `--accent`, texte noir, graisse 500. **Un seul par écran**, pour l'action qui fait avancer (Lancer, Figer et lancer l'analyse, Tester avec le jeu de démonstration). Après un premier calcul, « Relancer » redevient neutre.
* **Bouton destructif** (`.danger`) : texte `--flag`, bordure rouge à 45 %. Toujours confirmé par un second clic : le libellé change (« Cliquez à nouveau pour supprimer ») et revient après 4 s.
* **Bouton désactivé** : opacité 45 %, curseur interdit.
* **Lien** : `--accent`, souligné.
* **Champs** : fond `--bg`, bordure `--line`, rayon 6 px. Libellé au-dessus, en `--muted`, 13 px.
* **Cases à cocher** : 18 à 20 px, couleur `--accent`. Une case inutilisable est grisée avec la raison en infobulle.
* **Puce** (`.chip`) : 12 px, fond `--panel` ; variantes `.flag` (rouge) et `.ok` (vert, « RAS »).
* **Tuile** (`.tile`) : libellé `--muted` 12,5 px, valeur 22 px (19 px sur mobile).
* **Note** (`.note`) : bordure fine, bord gauche de 3 px. Rouge pour un avertissement (historique local). `.info` bleu pour une information (mode démo, écran verrouillé, première visite). Une note propose toujours la suite (lien ou bouton).
* **Liste de contrôles** (`.flags`) : une puce de couleur par ligne, `pass` vert, `warn` rouge, `info` gris, toujours avec le texte du contrôle.
* **Tableaux** : filets horizontaux seulement ; texte à gauche, nombres à droite ; dans un conteneur `.scroll` défilant horizontalement si besoin. `.kv` : tableau libellé / valeur, libellés en `--muted` sur 230 px.
* **Stepper** : 7 étapes numérotées avec un état sous chaque nom (vert = fait, rouge = à régler ou « À relancer », gris = à faire). Étape active en `--accent` avec un soulignement de 2 px qui glisse.
* **Navigation d'étape** (`.stepnav`) : en bas de chaque étape dès qu'un jeu est chargé, « ← étape précédente » à gauche, « Suivant : étape → » à droite, boutons neutres.
* **Notification** (`.status`) : en bas à droite, 620 px maximum (pleine largeur moins 16 px de marge sur mobile). Succès masqué après 5 s ; erreur conservée jusqu'à « Fermer ». Pendant un calcul : barre de progression et « Annuler ».
* **Zone de dépôt** (`.drop`) : bordure en tirets ; survol de fichier en `--accent` ; erreur en `--flag` avec le message juste en dessous (`.err-msg`).
* **État vide** (`.empty`) : panneau centré en `--muted`, avec toujours un lien vers l'étape qui débloque.
* **Menu** (Réglages) : panneau `--panel` sous le bouton, 340 px maximum.
* **Sélecteur de langue** : deux boutons EN | FR accolés ; la langue active a le fond `--panel` et le texte `--ink`.

## 6. Graphiques
* SVG dessinés à la main, sans bibliothèque. Couleurs lues dans les variables CSS.
* **Courbe observée** : `--ink`, trait plein. **Contrefactuel** : `--accent`, tirets. **Intervalle** : `--band`. **Pré-période** : fond `--shade`. **Intervention** : trait vertical pointillé. **Grille** : `--grid`, 4 graduations environ.
* Panneau principal 300 px de haut ; panneaux secondaires (effet ponctuel, effet cumulé) 170 px.
* Infobulle au survol : `--panel`, valeurs au format de la langue active.
* Mini-courbes des covariables : 150 × 28 px, `--muted`, trait `--accent` à l'intervention.
* Export PNG : fond noir, échelle × 2, titre en tête.

## 7. Mouvement
Uniquement pour la navigation et les retours d'action. Jamais sur les données.

| Élément | Animation | Durée |
|---|---|---|
| Soulignement du stepper | glisse vers l'étape active | 0,32 s |
| Changement d'écran (adresse `#…`) | fondu + montée de 8 px | 0,26 s |
| Notification | entrée en glissant depuis le bas / sortie en fondu | 0,22 s / 0,18 s |
| Menu Réglages | fondu d'ouverture | 0,16 s |
| Boutons | changement de couleur au survol, appui de 1 px | 0,15 s / 0,1 s |
| Flèches Précédent / Suivant | avancent de 3 px au survol | 0,2 s |

* Courbe d'accélération : `cubic-bezier(.2, .7, .2, 1)` pour les entrées, `ease` pour le reste.
* Pas d'animation quand l'écran se redessine sans changer d'adresse (saisie, changement de langue).
* `prefers-reduced-motion: reduce` coupe toutes les animations et transitions.

## 8. Contenu et langue
* Deux langues complètes, anglais et français, choisies par le sélecteur EN | FR. Toute nouvelle chaîne s'écrit dans les deux langues (`L('…', '…')`).
* Un bouton dit ce qui se passe (« Figer et lancer l'analyse », « Graphiques (PNG) »), pas « OK » ni « Valider ».
* Phrases courtes, vocabulaire du protocole et du Lexique (pré-période, covariable, statut H-A, hold-out, placebo, MDE).
* Français : espace insécable avant `%` et `:` ; virgule décimale (`+20,1 %`) ; dates `1 sept. 2026` à l'écran, `01/09/2026` dans les slides.
* Anglais : `+20.1%`, `1 Sep 2026`.
* Restent en anglais quelle que soit la langue : en-têtes des CSV, script R, valeurs enregistrées (statuts, catégories).
* Jamais de chiffre inventé : tout nombre affiché vient du moteur ou des données importées.

## 9. États
Chaque écran prévoit :
* **Vide** : explication courte et lien vers l'étape qui débloque. Écran Données vide : encadré « Première visite ? » avec la démo.
* **Calcul** : « Calcul en cours… » à l'endroit du futur résultat, plus la barre de progression dans la notification.
* **Erreur** : message près de sa cause (sous la zone de dépôt pour un import), en `--flag`.
* **Résultat périmé** : « À relancer » en `--flag` dans la section et dans le stepper.
* **Verrouillé** (fiche figée) : note `.info` neutre avec un lien « Amender la fiche ».
* **Mode démo** : note `.info` en tête de chaque étape, avec un lien pour sortir de la démo.

## 10. Accessibilité
* Focus visible sur tout élément interactif : contour `--accent` de 2 px, décalé de 2 px.
* Cibles de 40 px de haut minimum hors tableaux.
* Étape active signalée par `aria-current="step"` ; sélecteur de langue en `aria-pressed`.
* Messages d'erreur d'import en `role="alert"`.
* Textes longs coupés proprement (`overflow-wrap: anywhere` dans les tableaux libellé / valeur, notes, contrôles) : jamais de défilement horizontal de la page.
* Noms de colonnes importés toujours échappés avant affichage.

## 11. Responsive
* Un seul point de rupture : 720 px.
* Sous 720 px : en-tête non collant, boutons d'en-tête compacts (34 px), tuiles sur 2 colonnes, stepper défilant avec un dégradé à droite et l'étape active centrée, notification sur toute la largeur.
* Tableaux larges : défilement horizontal dans leur conteneur, jamais de la page.

## 12. Slides PowerPoint
Palette propre aux slides, plus douce que le noir pur de l'écran :

| Rôle | Valeur |
|---|---|
| Fond | `#121417` |
| Panneau | `#1B1E22` |
| Texte | `#E8EAED` |
| Secondaire | `#9AA1AA` |
| Filets | `#2C3137` |
| Accent | `#7FB0E0` |
| Alerte | `#FF6B6B`, fond `#3A1D21` |
| Contrôle passé | `#6FCF97` |

* Polices : Baikal Condensed (titres, 28 pt, réduits à 24 pt puis 21 pt pour les titres longs) et Calibri (texte).
* Format 16:9, quatre slides : fiche de test, une carte par covariable (30 au maximum), toutes les covariables sur un graphique (le KPI et les 10 covariables les plus incluses), résultat.
* Textes longs coupés avec « … » à une longueur fixe par zone ; noms de KPI raccourcis dans les titres.
* Effets arrondis à l'entier, confiance à une décimale. Langue des slides = langue du site.

## 13. À ne pas faire
* Pas de thème clair, pas de dégradé décoratif, pas d'effet verre, pas d'ombre hors notifications, menus et infobulles.
* Pas de second accent ni de couleur hors palette.
* Pas d'emoji ni d'icône décorative.
* Pas de bibliothèque ajoutée : tout tient dans `index.html` (seule exception, PptxGenJS chargée à la demande pour les slides).
* Pas d'animation des données, des graphiques ou des chiffres.
* Pas de verdict automatique : l'outil affiche, l'analyste conclut.

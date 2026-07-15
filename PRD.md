# Spark — Product Requirements Document

> Un second cerveau sans friction pour les pensées qu'on perdrait sinon.

**Statut** : pre-alpha
**Plateformes cibles (V1)** : iOS, Android (.NET MAUI)
**Stockage** : SQLite local, sur l'appareil
**Document** : PRD issu de la synthèse README + notes de version (V1–V4)

---

## 1. Pourquoi

Les meilleures idées n'arrivent pas au bureau. Elles surgissent en plein milieu d'une phrase lue chez quelqu'un d'autre, et disparaissent quelques secondes plus tard, parce que les noter demande trop d'étapes. Les outils qui *pourraient* les capter en exigent trop : taggage manuel, liaisons manuelles, organisation soigneuse. Résultat — la plupart des pensées ne sont jamais captées, et la plupart des gens abandonnent ces systèmes en quelques semaines.

Spark est construit pour **les autres 95 %** : ceux qui ont essayé Obsidian, Notion, et qui ont échoué à les maintenir.

## 2. Positionnement

**Spark est une application autonome.** Elle ne s'intègre à aucun outil existant (pas de plugin Obsidian, pas de connecteur Notion). Elle possède sa propre surface de capture, son propre stockage, et — plus tard — son propre moteur de connexions.

C'est un parti pris assumé : le différenciateur de Spark n'est pas « une énième app de notes », ce sont les **liens suggérés par l'IA et validés par l'humain**. Cette capacité est indépendante de l'endroit où vit le texte ; construire un éditeur complet pour l'héberger n'est pas le cœur de valeur, mais l'autonomie garantit le contrôle total de l'expérience et de la confidentialité.

**Mobile-first.** La promesse fondatrice — capturer *en lisant, en marchant, à moitié endormi* — ne vit que sur un téléphone (appareil de chevet, de poche, toujours sur soi). Le desktop arrive plus tard, pour les phases d'analyse et d'écriture qui appellent un grand écran.

## 3. La boucle produit

Trois battements, qui structurent toute la roadmap :

1. **Capture** — voix ou texte, à l'instant exact où la pensée frappe. Stockée brute, exactement comme elle a été dite.
2. **Connect** — Spark trouve les pensées anciennes qui ont un rapport, et suggère *comment* : confirme, contredit, nuance, évolue. L'utilisateur valide ou rejette chaque proposition.
3. **Write** — quand l'utilisateur est prêt, Spark dispose ses propres pensées en plan. La prose reste à écrire.

## 4. Principes & philosophie

- **Penser n'est pas expertiser.** Pas besoin de doctorat pour former de vraies intuitions sur un domaine. Spark leur donne un endroit où mûrir.
- **Préserver la voix.** Une réécriture propre vaut moins qu'une pensée brute et authentique. L'IA ne polit jamais les mots de l'utilisateur.
- **Friction là où elle compte, aucune là où elle n'en faut pas.** La capture doit être instantanée. Confronter ses propres idées doit demander un effort.
- **Tes mots restent tiens.** Jamais réécrits, jamais polis par l'IA. L'utilisateur reste l'auteur.

## 5. Personas cibles

- **Le lecteur qui oublie** — lit beaucoup, retient peu, voudrait relier ses intuitions au fil du temps.
- **Le penseur intermittent** — a des idées hors du bureau (marche, lit, demi-sommeil) mais n'a pas la discipline d'un système de notes manuel.
- **L'ancien utilisateur d'Obsidian/Notion** — a essayé, a abandonné par excès de friction de maintenance.

## 6. Roadmap — quatre versions

### V1 — Capture

**Objectif** : la boucle de capture la plus courte possible, mobile, voix comprise.

- Capture **texte** et **voix** (via STT native de l'OS : Apple Speech framework, Android SpeechRecognizer). Aucun moteur vocal maison.
- Pensée stockée **brute**, telle que dictée/écrite.
- **Source optionnelle** : une note peut être rattachée à une source (URL, passage collé, référence libre), apportée **manuellement** par l'utilisateur. Aucun lecteur de contenu interne ; l'ancrage à la source n'est jamais automatique.
- Stockage **local SQLite** sur l'appareil. Pas de compte forcé, pas de cloud pour la capture.

**Critère de succès V1** : un utilisateur peut capturer une pensée (voix ou texte) en moins de 5 secondes depuis son téléphone, et la retrouver.

### V2 — Connect (sans IA)

**Objectif** : donner un pouls au produit avant l'IA, en livrant des connexions par des moyens **non-IA**.

- **Liens lexicaux/statistiques** : détection de mots-clés, thèmes récurrents, similarité de surface (TF-IDF / embeddings légers). Spark propose des rapprochements que l'utilisateur valide ou rejette.
- **Graphe de connaissances** : cartographie des notes sous forme de graphe. L'utilisateur voit les îlots, les notes orphelines, les ponts possibles. Analyse **structurelle**, pas sémantique.
- **Entièrement on-device** : les petits modèles d'embedding tournent localement, aucune donnée ne quitte l'appareil.

**Critère de succès V2** : un utilisateur avec 50+ notes voit émerger des connexions pertinentes sans les avoir créées manuellement.

### V3 — Connect (IA)

**Objectif** : passer des connexions de **surface** aux connexions de **sens**.

- **Liens sémantiques** : l'IA comprend le sens des notes, pas seulement les mots qu'elles partagent.
- **Taxonomie des liens** : chaque connexion est qualifiée — *confirme*, *contredit*, *nuance*, *évolue* — exactement comme le README l'annonce.
- **Validation humaine préservée** : l'utilisateur approuve ou rejette chaque lien. La friction pensante est conservée.
- **Cloud, zero-retention** : le traitement IA est éphémère ; le fournisseur s'engage à ne ni stocker ni entraîner sur les données.

**Critère de succès V3** : un utilisateur reçoit des liens qualifiés (confirme/contredit/nuance/évolue) qu'il n'aurait pas trouvés par simple similarité lexicale.

### V4 — Write

**Objectif** : transformer un corpus de pensées en un plan utilisable.

- **Mise en plan** : Spark dispose les pensées de l'utilisateur en outline, regroupées par thème/tension.
- **Pas d'essais générés** : Spark structure, l'utilisateur écrit. Garantie « No generated essays » du README.
- **Cloud, zero-retention** : partage le moteur IA de V3.

**Critère de succès V4** : un utilisateur peut générer un plan cohérent à partir d'un cluster de pensées, sans que Spark écrive le texte à sa place.

## 7. Décisions structurantes

| Décision | Choix | Rationale |
|---|---|---|
| Autonome vs intégration | **Autonome, aucune intégration** | Contrôle total + confidentialité ; le différenciateur est orthogonal au stockage |
| Timing de l'IA | **V3, pas V1** | V1 valide d'abord la capture ; V2 livre des connexions sans IA |
| Plateformes V1 | **Mobile-first, iOS + Android** | La capture en mouvement n'existe pas sur desktop |
| Capture vocale | **Oui en V1, via STT native** | Cas d'usage phare (« à moitié endormi ») ; STT native mature et gratuite |
| Source d'une note | **Optionnelle, manuelle** | Préserve la zero-friction de capture ; pas de lecteur interne |
| Localisation de l'IA | **Cloud** | Qualité impossible à atteindre on-device sur mobile aujourd'hui |
| Modèle de confidentialité | **Zero-retention cloud** | « Tes données vivent sur ton appareil » reste vrai (stockage local) ; traitement IA éphémère |
| Write | **V4 dédiée** | Partage le moteur IA de V3 mais livrable séparé |

## 8. Gestion du volume grandissant

La question centrale de ce PRD : *comment gère-t-on le volume grandissant des liens/notes ?*

**Le problème réel.** Le stockage n'est pas le goulot (SQLite tient des millions de lignes). Le vrai point de rupture, c'est que **le modèle « tu valides chaque lien un par un » s'effondre à l'échelle** : à 50 notes, valider 10 suggestions est jouable ; à 5000, des centaines de liens noient l'utilisateur, le graphe devient illisible, et le différenciateur lui-même se casse.

**Le modèle de gestion du volume : passer de la validation lien-à-lien à la curation par thèmes.**

- **(a) Clusters/thèmes** — à grande échelle, l'IA ne propose plus 200 liens individuels mais regroupe les notes en thèmes émergents : *« 3 thèmes qui mûrissent, 2 tensions, 1 cluster orphelin »*. L'utilisateur engage au niveau du **thème**, pas du lien. La friction pensante du README est préservée sans noyade.
- **(d) Graphe hiérarchique** — niveaux de zoom (thèmes → clusters → notes) pour naviguer une structure, pas un écheveau plat. Rend (a) concret et navigable.
- **(c) Cycle de vie / décroissance** — les notes vieillissent ; les anciennes non resurgies s'archivent ou s'estompent. Le corpus s'auto-élague par pertinence et évite la pourriture lente.

**Exclu par défaut** : l'auto-liage par seuil de confiance sans validation humaine — il détruirait la promesse « friction where it counts ». Pourrait être activé optionnellement pour les liens triviaux, mais jamais comme mécanisme principal.

**Traduction en versions** : la validation lien-à-lien est le modèle de V2–V3 (volume faible/moyen) ; la curation par thèmes hiérarchisés avec cycle de vie devient le modèle dès que le volume le justifie (évolution continue au-delà de V3).

## 9. Confidentialité & données

- **Stockage** : SQLite local sur l'appareil. Les notes appartiennent à l'utilisateur, sont exportables, et ne nécessitent aucun compte.
- **Traitement IA (V3/V4)** : cloud, avec politique **zero-retention** — le fournisseur s'engage à ne ni stocker ni entraîner sur les données ; traitement éphémère, suppression immédiate après génération du résultat ; chiffrement en transit.
- **V2** : entièrement on-device. Aucune donnée ne quitte l'appareil.

**Tenue de la promesse README** :
- *« Local-first and private — your data lives on your device »* → **vrai** : les données reposent sur l'appareil (stockage local).
- *« Your words stay yours »* → **vrai** : l'IA ne réécrit jamais les mots de l'utilisateur.
- *« Privé »* → **tenu par zero-retention** : la confidentialité repose sur l'éphémérité du traitement cloud, pas sur un air-gap local. Ce point doit être communiqué honnêtement aux utilisateurs (pas de promesse de hors-ligne absolu pour l'IA).

## 10. Risques & tensions acceptées

- **V3 et V4 partagent le même moteur IA.** Les séparer en deux versions duplique une partie de l'infrastructure IA. Choix assumé au profit d'une roadmap plus lisible et d'un livrable V3 recentré sur les connexions.
- **« Privé » repose sur zero-retention cloud**, pas sur un traitement 100 % local. Honnête mais plus fragile qu'un air-gap : dépend de la politique réelle du fournisseur d'IA.
- **V1 livrée sans connexions** : une app de capture seule est, par définition, « une énième app de notes » jusqu'à V2. Risque d'abandon utilisateur avant que la valeur de connexion n'apparaisse. À mitiger par une cadence de release V1 → V2 courte.
- **Cloud sur mobile** : la qualité de l'IA V3/V4 dépend de la connectivité réseau. Expérience dégradée hors-ligne.

## 11. Hors périmètre

- **Intégration avec Obsidian, Notion, ou tout autre outil tiers.** Spark est autonome.
- **Lecteur de contenu interne** (pas de lecture d'ePub/PDF/articles dans Spark). La source est apportée manuellement par l'utilisateur.
- **Génération de prose / essais.** Spark structure, n'écrit jamais à la place de l'utilisateur.
- **IA on-device en V3/V4.** Trop peu performante sur mobile aujourd'hui.
- **Desktop avant V2/V3.** Le desktop a tout son sens pour le graphe et l'écriture, mais pas pour la capture initiale.

---

*Document vivant. Toute évolution majeure des décisions de la section 7 doit être tracée.*

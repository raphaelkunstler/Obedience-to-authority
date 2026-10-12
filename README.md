# Étude sur la mémoire et l'apprentissage : réplication en ligne de l'expérience de Milgram

Site statique, sur le modèle du site de l'étude SAV (`etude-sav`). Le sujet vit, à l'écran et au casque, la séance de la « nouvelle ligne de base » de Milgram (condition 5 : rétroaction vocale, l'élève signale un problème cardiaque) : accueil par l'expérimentateur, présentation de l'autre participant, reçu et paiement, discours sur la mémoire et la punition, tirage au sort truqué, installation de l'élève, présentation du générateur, choc échantillon de 45 volts, leçon d'entraînement, leçon normale, incitations, fin de séance.

Aucun serveur, aucune base de données, aucune clé d'API. Toutes les répliques sont dans `index.html`.

## Contenu du dépôt

| Fichier | Rôle |
| --- | --- |
| `index.html` | Le parcours complet. Page à donner aux sujets, et la seule à modifier. Textes et réglages : premier `<script>` ; moteur : second `<script>`. |
| `img/` | Portraits de John Williams (expérimentateur) et de James McDonough (« M. Wallace », l'élève), tirés du générique du film *Obedience* (1962), et plans du film utilisés comme décor de chaque étape. |
| `audio/` | Emplacement des enregistrements de l'élève (facultatif ; voir `audio/LISEZMOI.md`). Vide : la synthèse vocale du navigateur prend le relais. |
| `integration-qualtrics.md` | Insertion dans Qualtrics et champs Embedded Data. |
| `.nojekyll` | Empêche GitHub de transformer les fichiers. À garder. |

## Ce qui est repris de Milgram, et d'où

| Élément | Source |
| --- | --- |
| Répliques de l'accueil, du discours (Cantor, *The Teaching-Learning Process*), du tirage, de l'installation de l'élève, du générateur, du choc échantillon et des consignes | Transcription du film *Obedience* (mai 1962), complétée par Blass (2004), reconstitution de la condition 5. Traduction française de ces textes. |
| Les 25 paires de la leçon normale et leurs quatre choix | Blass (2004), transcription ; version française : la « Partition de l'expérimentateur » du Jeu du Non. La ligne LOW n'apparaît pas dans la transcription : ses choix sont reconstitués. |
| Schéma des réponses de l'élève | Blass (2004) : justes à BLUE, NICE, FAST, GOLD, SAD, NEW, QUIET, puis BLUE au second passage ; erreurs ailleurs. La première liste mène donc à 270 volts, comme dans la transcription. |
| Leçon d'entraînement : 10 paires, 3 justes, 7 erreurs, choc maximal 105 volts | Milgram (1974), note sur la leçon d'entraînement (« STRONG arm, BLACK curtain… »). Les quatre choix et la place des trois réponses justes sont reconstitués. |
| Protestations de l'élève, niveau par niveau ; silence au-delà de 330 volts ; plus de réponses à partir de 300 volts | Milgram (1974, p. 56-57). |
| Incitations 1 à 4, dans l'ordre, reprises au début à chaque nouvelle occasion de réticence ; arrêt après la quatrième | Milgram (1974, p. 21-22). |
| Incitations spéciales (lésions, volonté de l'élève), réponse sur la responsabilité, sur l'argent, sur « jusqu'où » | Milgram (1974) ; film *Obedience* ; transcriptions des séances. |
| Consigne du silence (« environ cinq secondes »), « continuez avec le dernier interrupteur », arrêt après trois chocs à 450 volts | Blass (2004) ; Milgram (1974). |
| Générateur : 30 interrupteurs de 15 à 450 volts, libellés par groupes de quatre, XXX, plaque « Shock generator, type ZLB, Dyson Instrument Company », lampe rouge au-dessus de l'interrupteur, voyant bleu, voltmètre, bourdonnement, déclics de relais, interrupteur laissé en position intermédiaire après usage, boîte de réponse 1-2-3-4 | Blass (2004) ; plans du film. |
| Mesures : niveau, latence et durée de chaque choc ; écarts à la procédure | Le « event recorder » de Milgram, décrit dans le film. |

## Ce qui ne peut pas être repris tel quel

- **Les voix.** L'expérimentateur et l'élève parlent avec la synthèse vocale du navigateur ; la voix exacte dépend de l'ordinateur du sujet. Les cris (« cri de douleur ») sont mal rendus par la synthèse. Pour une passation réelle, il faut enregistrer les protestations de l'élève, comme Milgram l'avait fait sur bande : voir `audio/LISEZMOI.md`.
- **Le choc échantillon** est remplacé par le bourdonnement du générateur (plus fort), un éclair à l'écran et une vibration sur les appareils qui en ont. Le dialogue est conservé (« Non, en fait, c'était 45 volts »).
- **La parole du sujet.** Par défaut, ce que dit le sujet (lecture des lignes, « exact », « faux », annonce du voltage, bonne paire) passe par des boutons qui prononcent la phrase avec la voix qu'il a choisie. Avec `?voix=oral`, le sujet prononce lui-même la phrase au micro, puis clique sur « C'est dit ».
- **Les réticences.** Le sujet s'adresse à M. Williams par écrit (zone « Parler à M. Williams », avec trois phrases toutes faites). Une inaction prolongée pendant la leçon (20 secondes par défaut) compte aussi comme une hésitation et appelle une incitation. Le classement des paroles du sujet (question de procédure, incitation spéciale, réticence) se fait par mots clés : liste `REPONSES` dans `index.html`.
- **Les corrections de procédure.** L'expérimentateur corrige les écarts (choc sans mauvaise réponse, mauvais interrupteur, « exact » sur une réponse fausse, passage à la ligne suivante sans punition). C'est une décision de mise en œuvre : dans les enregistrements, Williams ne corrige pas toujours. `?correction=0` supprime ces corrections ; les écarts restent enregistrés.
- **Le cadre.** L'expérience est en ligne : le « laboratoire » est représenté par les plans du film. Les noms sont ceux de l'original (M. Williams, M. Wallace) ; l'expérimentateur dit travailler avec le responsable de la recherche (`PERSONNES.prof`).

## Droits sur les images

Les portraits et les plans viennent du film *Obedience* (© 1965 Stanley Milgram ; © renouvelé 1993 Alexandra Milgram ; distribution Penn State Media Sales). Leur usage dans un dépôt public et devant des sujets doit être vérifié avant toute passation, avec le service juridique de l'université ou l'ayant droit. Les remplacer ne demande que de déposer d'autres fichiers sous les mêmes noms dans `img/`.

## Visibilité du dépôt

Le nom du dépôt (`Obedience-to-authority`) apparaît dans l'adresse GitHub Pages, que les sujets voient, et le dépôt public rend le script lisible, tirage truqué compris. Avant toute passation : héberger le site sous un nom neutre (un autre dépôt, comme pour `etude-sav`, ou un serveur de l'université).

## Mise en ligne avec GitHub Pages

« Settings », « Pages », « Deploy from a branch », branche `main`, dossier `/ (root)`. L'adresse prend la forme `https://raphaelkunstler.github.io/Obedience-to-authority/`.

## Adresses utiles

| Ajout à l'adresse | Effet |
| --- | --- |
| *(rien)* | Parcours complet, pour les sujets. |
| `?pid=…&cond=…` | Identifiant du participant et condition, transmis par Qualtrics. |
| `?lang=en` | Version anglaise, avec les formulations originales de Milgram et du film. |
| `?voix=oral` | Le sujet prononce lui-même ses phrases. |
| `?coeur=0` | L'élève ne mentionne pas de problème cardiaque (pas de « mon cœur » dans les protestations). |
| `?correction=0` | Pas de correction des écarts de procédure. |
| `?raccourcis=0` | Pas de phrases toutes faites sous « Parler à M. Williams ». |
| `?soustitres=0` | Les paroles de l'élève ne s'affichent pas par écrit (seulement « voix dans la pièce voisine »). |
| `?inaction=20` | Délai d'inaction, en secondes, avant une incitation. |
| `?etape=…` | Accès direct : `arrivee`, `discours`, `tirage`, `sanglage`, `generateur`, `consignes`, `entrainement`, `session`, `fin`. |
| `?rapide` | Essais : voix coupées, délais très courts. |
| `?debug` | Panneau de test : journal en direct, saut entre les étapes, copie du journal. |
| `?audio=0` | Ignore les enregistrements de `audio/`. |
| `?retour=https://…` | Adresse où renvoyer le sujet après « Continuer », si le site n'est pas dans Qualtrics. |

Les paramètres se combinent avec `&` : `index.html?pid=R_123&lang=en&voix=oral`.

## Avant la première passation

1. Remplir l'objet `CONSENT` (comité d'éthique, numéro et date de l'avis, durée de conservation, adresse du DPO) : les champs restent surlignés en jaune tant qu'ils sont vides.
2. Vérifier `PERSONNES` (nom du responsable cité par Williams, montant de la gratification affiché sur le reçu et le chèque).
3. Enregistrer les protestations de l'élève (`audio/`).
4. Prévoir le débriefing dans Qualtrics, après le site : explication complète, réconciliation avec l'élève (Milgram faisait entrer McDonough), choix de conserver ou de retirer les données.

## Données

Le site n'envoie rien à GitHub. Pendant la passation, le journal complet est transmis à la page parente par `postMessage` après chaque événement (source `etude-memoire`). Champs principaux : `voltageMax`, `obeissant` (trois chocs à 450 volts), `endReason` (`obeissance`, `refus`, `duree`), `n450`, `nIncitations`, `nIncitationsSpeciales`, `nReticences`, `nCorrections`, `nEcarts`, `estimationEchantillon`, `chocs` (une ligne par choc : leçon, ligne, passe, volts, voltage attendu, durée d'appui en ms, latence depuis la réponse de l'élève, voltage annoncé ou non, choc hors procédure), `sujetMessages`, `transcript`, `events`.

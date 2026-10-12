# Intégration dans Qualtrics

## 1. Héberger le site

`index.html` est une page statique autonome. Publiée par GitHub Pages, elle a pour adresse `https://raphaelkunstler.github.io/Obedience-to-authority/` (à remplacer par un hébergement au nom neutre avant les passations : voir le README). Pour tester hors Qualtrics, ajoutez `?debug`.

## 2. Déclarer les champs dans le Survey Flow

Avant le bloc de la séance, un élément **Embedded Data** avec les champs suivants, laissés vides :

`mg_fin`, `mg_obeissant`, `mg_voltage_max`, `mg_n450`, `mg_n_incitations`, `mg_n_incitations_speciales`, `mg_n_reticences`, `mg_n_ecarts`, `mg_n_corrections`, `mg_estimation`, `mg_chocs`, `mg_sujet`, `mg_transcript`, `mg_events`.

En mise en page « Simple layout », Qualtrics exige le préfixe `__js_` pour les champs écrits par JavaScript : déclarez aussi `__js_mg_fin`, etc. Le code ci-dessous essaie les deux API ; vérifiez sur une réponse test laquelle des deux colonnes se remplit.

## 3. La question qui contient la séance

Une question **Text / Graphic**. Dans l'éditeur HTML :

```html
<iframe id="etude"
  src="https://raphaelkunstler.github.io/Obedience-to-authority/?pid=${e://Field/ResponseID}&cond=${e://Field/cond}"
  style="width:100%; height:900px; border:0;" allow="autoplay; microphone"></iframe>
```

Ajoutez `&lang=en` pour la version anglaise, `&voix=oral` pour que le sujet prononce lui-même ses phrases. La séance demande au moins 1 100 pixels de large : réglez le thème de l'enquête en pleine largeur, ou ouvrez le site dans un nouvel onglet avec `&retour=` suivi de l'adresse de la suite de l'enquête.

## 4. Le JavaScript de la question

```js
Qualtrics.SurveyEngine.addOnload(function () {
  var q = this;
  q.hideNextButton();
  function setED(name, value) {
    value = String(value == null ? '' : value);
    try { Qualtrics.SurveyEngine.setJSEmbeddedData(name, value); } catch (e) {}
    try { Qualtrics.SurveyEngine.setEmbeddedData(name, value); } catch (e) {}
  }
  window.addEventListener('message', function (ev) {
    var d = ev.data;
    if (!d || d.source !== 'etude-memoire') return;
    setED('mg_fin', d.endReason || (d.ended ? 'oui' : 'non'));
    setED('mg_obeissant', d.obeissant ? 1 : 0);
    setED('mg_voltage_max', d.voltageMax);
    setED('mg_n450', d.n450);
    setED('mg_n_incitations', d.nIncitations);
    setED('mg_n_incitations_speciales', d.nIncitationsSpeciales);
    setED('mg_n_reticences', d.nReticences);
    setED('mg_n_ecarts', d.nEcarts);
    setED('mg_n_corrections', d.nCorrections);
    setED('mg_estimation', d.estimationEchantillon);
    setED('mg_chocs', JSON.stringify(d.chocs));
    setED('mg_sujet', (d.sujetMessages || []).map(function (m) { return Math.round(m.t / 1000) + 's [' + m.volts + ' V] ' + m.texte; }).join('\n'));
    setED('mg_transcript', d.transcript);
    setED('mg_events', JSON.stringify(d.events));
    if (d.ended) q.showNextButton();
    if (d.continuer) q.clickNextButton();
  });
});
```

Le site envoie le journal complet après chaque événement : si le sujet quitte en cours de route, ce qui a eu lieu jusque-là est conservé. Le journal d'une séance complète peut dépasser la taille admise pour un champ Embedded Data (environ 20 000 caractères selon les versions de Qualtrics, à vérifier) : `mg_events` peut alors être tronqué, les autres champs restent complets.

## 5. Ce qui est enregistré

`mg_fin` vaut `obeissance` (trois chocs à 450 volts), `refus` (nouvelle réticence après la quatrième incitation) ou `duree` (50 minutes). `mg_voltage_max` est le choc le plus élevé donné pendant la leçon. `mg_chocs` contient un objet par choc : `lecon` (`entrainement` ou `normale`), `ligne`, `passe`, `volts`, `attendu` (voltage prescrit par la procédure), `duree` (temps d'appui sur l'interrupteur, en ms), `latence` (délai depuis la réponse de l'élève, en ms), `annonce` (le voltage a-t-il été annoncé), `horsProcedure`.

Principaux événements de `mg_events` (temps `t` en ms depuis l'ouverture de la page) : `consentement`, `accueil`, `etape`, `recu_signe`, `tirage`, `echantillon`, `estimation`, `lecon_debut`, `liste_lue`, `ligne_lue`, `reponse_eleve`, `jugement`, `annonce`, `choc`, `paire_lue`, `protestation`, `parole_exp` (ce que le sujet dit à l'expérimentateur), `reticence` (avec `source` = `parole` ou `inaction`), `incitation` (`kind` = `reguliere` avec son rang, ou `speciale`), `reponse_procedure`, `ecart` (avec `kind` : `saut_punition`, `paire_non_lue`, `exact_non_dit`, `exact_sur_faux`, `faux_sur_exact`, `choc_hors_procedure`, `choc_repete`, `trop_bas`, `trop_haut`, `voltage_non_annonce`, `annonce_hors_procedure`, `paire_avant_choc`), `correction`, `reprise` (le sujet reprend après des incitations), `consigne_silence`, `consigne_dernier`, `fin`, `continuer`.

## 6. Le débriefing

Dans Qualtrics, après le questionnaire : explication complète (l'élève est un complice, il n'a reçu aucun choc ; les protestations sont enregistrées), présentation de l'élève réconcilié si possible (Milgram faisait entrer McDonough : « You don't feel too bad, now, do you? »), et choix de conserver ou de retirer les données, comme dans l'étude SAV.

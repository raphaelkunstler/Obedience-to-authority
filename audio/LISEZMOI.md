# Enregistrements de l'élève

Milgram faisait entendre des protestations enregistrées sur bande, coordonnées au niveau du choc. Le site fait de même si les fichiers existent ; sinon il emploie la synthèse vocale du navigateur, qui rend mal les cris.

Un fichier par niveau, nommé d'après les volts sur trois chiffres, dans `audio/fr/` ou `audio/en/` :

`eleve-075.mp3`, `eleve-090.mp3`, `eleve-105.mp3`, `eleve-120.mp3`, `eleve-135.mp3`, `eleve-150.mp3`, `eleve-165.mp3`, `eleve-180.mp3`, `eleve-195.mp3`, `eleve-210.mp3`, `eleve-225.mp3`, `eleve-240.mp3`, `eleve-255.mp3`, `eleve-270.mp3`, `eleve-285.mp3`, `eleve-300.mp3`, `eleve-315.mp3`, `eleve-330.mp3`.

Chaque fichier contient toute la protestation de ce niveau (texte dans `PROTESTATIONS`, `index.html`), cri compris, et remplace la première réplique ; s'il existe, enregistrez donc la protestation entière et supprimez les répliques suivantes du niveau dans `PROTESTATIONS`, ou laissez-les : elles seront alors dites en plus par la synthèse. Le plus simple est d'enregistrer la protestation entière et de réduire l'entrée du niveau à une seule réplique.

Au-delà de 330 volts, l'élève se tait : pas de fichier.

Pour l'enregistrement, Milgram (1974) décrit une voix d'homme d'âge mûr, à travers une cloison. Un léger filtrage (passe-bande 300-3400 Hz) imite la pièce voisine.

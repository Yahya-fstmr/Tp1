# Registre des failles

Application : <<Mes notes >> - gestion des notes des étudiants.

## Acteurs 

**Légitimes**
- Étudiant : consulte ses propres notes et sa moyenne.
- Enseignant : saisit et modifie les notes de ses matiers.
- Administrateur : gère les comptes et le serveur.

**Attaquants potentiels**
_ Éetudiant : veut modifier sa note ou lire celle des autres (il a un compte légitime).
- Attaquqnt externe : chercher à voler des comptes, surtout ceux des enseignants.
- Attaquqnt sur le réseau : sur un Wi-Fi public, il écoute ou redirige le trafic.

## Bien à protéger (du plus au moins sensible)


1. **Mots de passe et comptes enseignants/adminisrateur** : celui qui les controle peut modifier. C'est la port d'entrée vers les autres biens.
2. **Intégrité** : une note modifiée à tort fausse un résult officiel.
3. **Confidentialité des notes et des données personnelles** : atteinte à la vie privée des étudiants.
4. **Disponibilité du servicee** : genante surtout à la publication des résultats, mais temporaire et sans modification des données.

## Points d'entrée


- Page de connexion (idenfiant et mot de passe).
- Formulaire de saisie des notes (espace enseignant).
- L'API ('/api/...') et ses parmètres, appelable directement sans passer par les pages.
- Le réseaux : Wi-Fi public, DNS.
- Les dépendance nmp (chaine d'approvisionnement) : 'nmp instal' télécharge et exécute du code tiers.
- La base de donnée, si elle est exposée sur Internet.

## Scénarios d'attaque


1. **Un étudiant essaie de modifier sa propre note en envoyant directement une requete à l'API de saise, sans passer par l'espace enseignant.**
*Pourquoi :* c'est la menace la plus réaliste, car l'étudiant a un motif et un compte légitime. Elle vise l'intégrité des notes via l'API. Elle montre que cacher un bouton ne protège rien : le serveur doit vérifier les droits à chaque requete.
2. **Un attaquant essaie de voler le mot de passe d'un enseignant en lui envoyent un faux e-mail << Votre note a été modifiée >> avec un lien vers un faux site de connexion.**
*Pourquoi :* il vise le bien n° 1 (les comptes), qui ouvre la porte à tout le reste. Il n'exige aucune faille technique : il tromp l'humain, maillon souvent le plus faible. Il rejoint l'exercice 2 du TD (liens piégés).
3. **UN attaquant connecté au meme Wi-Fi qu'un étudiant, dans un café, essaie d'intercepter sa connexion en falsifiant les réponses DNS pour le rediriger vers un faux serveur.**
*Pourquoi :* il couvre un point d'entrée différent, le réseau, et non l'application elle-meme. Il s'appuie sur ce qu'on a vu avec badssl (certificat invalide) et judtfie l'usage du HTTPS.

## Synthèse 

|Scénaro | Bien visé | Point d'entrée |
|---|---|---|
| 1 | Intégrité des notes | API |
| 2 | Comptes et mots de passe | Connexion, e-mail |
| 3 | Confidentialité de la session | Réseau, DNS |

# Registre des failles

##Acteurs
-Étudiant (légitime) : consulte ses notes.
-Enseignant (légitime) : saisit et modifie les notes.
-Administrateur (légitime) : gère les comptes et le serveur.
-Étudiant malveillant : veut modifier ou voir les notes des autes.
-Attaquant externe : chercher à voler des comptes ou des données.

## Bien à protéger
1. Mots de passe et session des utilisateurs
2. Les notes (intégrité : personne ne doit les modifier à tort)
3. Données personnelles des étudiants
4. Comptes enseignants et administrateur
5. Disponibilité du service

## points d'entrée
- Formulaire de connextion
- Pages de saisie des notes (espace enseignant)
- L'API (route /api/...) et ses paramètres
- Les dépendances npm (chaine daapprovisionnement)
- Le réseau (Wi-Fi public, DNS)
- La base de données, si elle est exposée

## Scénarios d'attaque 
1. Un étudiant essaie de modifier sa note en appelant directement l'API de saisie, sans passer par l'espace enseignant.
2. Un attaquant essaie de voler un mot de passe en envoyant un faux e-email avec un lien piégé vers un faux site.
3. Un attaquant sur le Wi-Fi d'un café essaie d'intercepter la connexion en falsifiant les réponses DNS.

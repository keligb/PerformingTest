# PerformingTest

### Julien Arbellini, Kelig Brindeau, Léa Ifergan, Waruny Rajendran 28/06/2022 4IW3

# Test 1 : Anybet
Lien : http://vps-a9e5c013.vps.ovh.net/

### Description du projet

Il s'agit d'un site de paris en ligne. 
Les utilisateurs ont la possibilité de créer des paris sur le sujet qu'il veulent.
Il y a une partie front office et back office.
La partie front office permet de parier, créer des paris et gérer son profil utilisateur et sa cagnotte.
La partie back office permet de gérer les utilisateurs, modérer la création des paris, gérer les événements et les catégories des paris, visualiser les statisques du site sous forme de graphiques.

Le site n'est pas encore hébergé sur un serveur.


### Architecture de l'application

Le site est structuré suivant le modèle MVC. Le langage principal utilisé est le PHP associé au framework Symfony. Le front est créé avec twig.
Notre site utilise Stripe pour le paiement, SASS pour le style, SendinBlue pour l'envoi des mails.

### Exigences du test

Déterminer le seuil de performance 

Nous avons choisi de réaliser un stress test car le site nous allons tester est un site de pari en ligne, et il n'a pas vocation d'accueillir chaque client sur une longue durée.
Au contraire notre site à plutôt vocation à accueillir un nombre élevé d'utilisateurs à un moment donné (ex : soirée de match de foot). C'est ainsi que le stress test est un test pertinent car il est en adéquation avec le mode de fonctionnement de notre site. De ce fait, nous avons défini qu'il serait préférable que le site réponde à certaines exigences notamment le délai de réponse lors des différentes étapes d'utilisation du site. 

| Business Transactions | User Load | Response Time | Transactions per hour |
|--------------|:-----------:|:------------:|:------------:|
| Access login page | 200 | 1 | 500 |
| Access register page | 100 | 1 | 300 |
| Parier | 200 | 1 | 1000

### Environnement de test

Environnement de test : Debian

- Nombre de coeurs : 1
- RAM : 2Go
- Stockage : 40Go

### Planification des tests

1 - La structure de notre site implique l'appel de ressources extérieures (Stripe, ChartJS, ...) qui peuvent ne pas fonctionner et générer des latences, des problèmes non controlables.

2 - Nous savons que les sites de paris en ligne sont généralement très fréquentés. Notre site ayant pour plus value de donner la possibilité à un utilisateur de créer ses propres paris et de gagner de l'argent en tant que créateur, nous nous attendons à un trafic élevé.
En fonction du trafic sur le site, nous adapterons notre modèle de test.

3 - Pour tester notre site nous aurons besoin de réaliser un stress test pour simuler un pic de charge. 

4 - Métrics : 
- utilisation du CPU/mémoire : échec à partir de 95% d'utilisation
- temps de réponse moyen : échec à partir de plus de 5 sec
- taux d'erreur : aucune erreur

### Étapes des tests

| Step # | Business Process Name : Parier
|--------------|:-----------:
| 1 | HomePage
| 2 | Login
| 3 | Select Choice
| 4 | Enter stake
| 5 | Confirm payment
| 6 | Payement
| 7 | Logout

### Exécution des tests

| Test Run | Test Scenario Summary |
|--------------|:-----------:|
| Cycle 1 - Run 1 | Stress Test - 20 minutes test with peak load |
| Cycle 1 - Run 2 | Stress Test - 20 minutes test with 150% of peak load |


|    | Test Details |
|--------------|:-----------:|
| Purpose | The processing of bets as they are posted will be examined to determine if the system can maintain response times below the maximum expected load. This test is designed to test for a surge in load. Over a short period of time, a large load is sent to simulate a massive influx of users. Unlike Stress Testing, the objective is not to crash the application. We want to determine if it can support a specific type of use. |
| No. of Tests | 1 (2 tests per cycle) |
| Duration | 20 x 2 |
| Scripts |  |
| Scenario Name | Stress Test Scenario |
| User Load / Volume | 200 Vusers Load |
| Entry Criteria | 1. The code should be stable and functionally verified <br/> 2. Test Environment should be stable and ready to use <br/> 3. Test Data should be available <br/> 4. All the NFRs should be agreed with the project <br/> 5. Test scripts should be ready to use |
| Validation Criteria |  1. The mean of the response time should be below 1.5 sec <br/> 2. The error rate should be below 5%
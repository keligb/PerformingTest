# PerformingTest

### Julien Arbellini, Kelig Brindeau, Léa Ifergan, Waruny Rajendran 28/06/2022 4IW3

# Test 1 : Anybet
Lien : localhost

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

Déterminer le seuil de performance // a reformuler 
Stress test

| Business Transactions | User Load | Response Time | Transactions per hour |
|--------------|:-----------:|:------------:|:------------:|
| Access login page | 200 | 1 | 500 |
| Access register page | 100 | 1 | 300 |
| Parier | 200 | 1 | 1000

### Environnement de test

Environnement de test : local

- Puce Apple M1
- RAM : 16go
- OS : MacOs Monterey

### Planification des tests

2 - Nous savons que les sites de paris en ligne sont généralement très fréquentés. Notre site ayant pour plus value de donner la possibilité à un utilisateur de créer ses propres paris et de gagner de l'argent en tant que créateur, nous nous attendons à un trafic élevé.
En fonction du trafic sur le site, nous adapterons notre modèle de test.

3 - Pour tester notre site nous aurons besoin de réaliser des tests d'endurance, de volumes de stress et de spike testing pour simuler un pic de charge.

4 - Métrics : 
- utilisation du CPU/mémoire : échec à partir de 95% d'utilisation
- temps de réponse moyen : échec à partir de plus de 5 sec
- taux d'erreur : échec à partir de

### Étapes des tests

| Step # | Business Process Name : Parier
|--------------|:-----------:
| 1 | HomePage
| 2 | Login
| 3 | Select Choice
| 4 | enter stake
| 5 | Confirm payment
| 6 | Payement
| 7 | Logout

### Exécution des tests

| Test Run | Test Scenario Summary |
|--------------|:-----------:|
| Smoke Test | To validate the performance test scripts and monitors |
| Cycle 1 - Run 1 | Spike Test - 1 Hour test with peak load |
| Cycle 1 - Run 2 | Repeat Spike Test - 1 Hour test with peak load |
| Cycle 1 - Run 3 | Stress Test - 1 Hour test with 150% of peak load |
| Cycle 2 - Run 1 | Spike Test - 1 Hour test with peak load |
| Cycle 2 - Run 2 | Repeat Spike Test - 1 Hour test with peak load |
| Cycle 2 - Run 3 | Stress Test - 1 Hour test with 150% of peak load |


|    | Test Details |
|--------------|:-----------:|
| Purpose | The processing of bets as they are posted will be examined to determine if the system can maintain response times below the maximum expected load. This test is designed to test for a surge in load. Over a short period of time, a large load is sent to simulate a massive influx of users. Unlike Stress Testing, the objective is not to crash the application. We want to determine if it can support a specific type of use. |
| No. of Tests | 4 (2 tests per cycle) |
| Duration |  |
| Scripts |  |
| Scenario Name | Spike Test Scenario |
| User Load / Volume | 200 Vusers Load |
| Entry Criteria | 1. The code should be stable and functionally verified <br/> 2. Test Environment should be stable and ready to use <br/> 3. Test Data should be available <br/> 4. All the NFRs should be agreed with the project <br/> 5. Test scripts should be ready to use |
| Validation Criteria |  1. The mean of the response time should be below 1.5 sec <br/> 2. The error rate should be below 5%







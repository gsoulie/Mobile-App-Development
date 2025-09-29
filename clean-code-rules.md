# Introduction au Clean Code

Le **Clean Code** est une approche de développement logiciel qui vise à rendre le code plus lisible, maintenable et évolutif. En adoptant les principes du Clean Code, nous pouvons améliorer la qualité de nos livrables, réduire les bugs et faciliter l'intégration de nouvelles ressources dans le projet. Ce document présente de manière synthétique et concrète les principes **SOLID**, **KISS** et **DRY**, accompagnés d'exemples et d'images pour faciliter leur mémorisation.

## Objectifs du Clean Code

- **Réduire la complexité** : Un code simple est plus facile à comprendre et à maintenir.
- **Augmenter la qualité** : Un code propre est moins sujet aux bugs et aux erreurs.
- **Faciliter l'évolution** : Un code bien structuré est plus facile à modifier et à étendre.
- **Améliorer la maintenance** : Un code lisible permet de corriger rapidement les problèmes.
- **Intégrer de nouvelles ressources** : Un code clair facilite l'intégration de nouveaux développeurs.

## Soyez acteur de la qualité

Il est crucial de ne pas hésiter à corriger et refactoriser le code, même si ce n'est pas nous qui l'avons écrit initialement. Chaque membre de l'équipe doit contribuer à maintenir un haut niveau de qualité.

---

# Principes SOLID

Les principes **SOLID** sont des concepts fondamentaux en développement logiciel qui visent à améliorer la qualité et la maintenabilité du code.

## 1. Single Responsibility Principle (SRP)

**Concept** : Une classe / composant / fonction, doit avoir une, et une seule, raison de changer, **une seule responsabilité**.

**Exemple concret** :
Imaginez une classe `Voiture` qui gère à la fois la conduite et la gestion des passagers. Si vous devez modifier la manière dont les passagers sont gérés, vous risquez de casser la logique de conduite.

**Image mentale** :

*Un couteau suisse avec une seule lame. Chaque outil (lame) a une seule fonction.*

**Exemple détaillé**
Dans cet exemple, la classe ````UserManager```` gère à la fois l'authentification et l'envoi de notifications, ce qui viole le principe SRP. Nous allons séparer ces responsabilités en deux classes distinctes.

<details>
  <summary>Code de l'exemple</summary>

````typescript
class UserManager {
    authenticate(username: string, password: string): boolean {
        // Logique d'authentification
        return true;
    }

    sendEmail(user: string, message: string): void {
        // Logique d'envoi d'email
        console.log(`Sending email to ${user}: ${message}`);
    }
}

>>>>> Refactorisé de la manière suivante :

class AuthenticationManager {
    authenticate(username: string, password: string): boolean {
        // Logique d'authentification
        return true;
    }
}

class NotificationManager {
    sendEmail(user: string, message: string): void {
        // Logique d'envoi d'email
        console.log(`Sending email to ${user}: ${message}`);
    }
}


````  
</details>



**Conclusion** : En séparant les responsabilités, vous rendez le code plus modulaire et facile à maintenir.

## 2. Open/Closed Principle (OCP)

**Concept** : Les entités logicielles doivent être ouvertes pour extension, mais fermées pour modification.

**Exemple concret** :
Si vous avez une classe `Calculatrice` qui effectue des opérations mathématiques de base, vous devriez pouvoir ajouter de nouvelles opérations (comme la racine carrée) sans modifier le code existant.

**Image mentale** :
*Un livre où vous pouvez ajouter des pages (extensions) sans réécrire les pages existantes.*

**Exemple détaillé**

Dans cet exemple, la classe ````ReportGenerator```` doit être modifiée chaque fois qu'un nouveau format de rapport est ajouté. Nous allons utiliser une interface pour permettre l'ajout de nouveaux formats sans modifier la classe existante.

<details>
  <summary>Code de l'exemple</summary>

````typescript
class ReportGenerator {
    generatePDF(data: any): void {
        // Logique de génération de PDF
        console.log("Generating PDF report");
    }

    // Si vous devez ajouter un nouveau format, vous devez modifier cette classe
    generateExcel(data: any): void {
        // Logique de génération d'Excel
        console.log("Generating Excel report");
    }
}

>>>> Refactorisé de la manière suivante

interface ReportFormat {
    generate(data: any): void;
}

class PDFReport implements ReportFormat {
    generate(data: any): void {
        // Logique de génération de PDF
        console.log("Generating PDF report");
    }
}

class ExcelReport implements ReportFormat {
    generate(data: any): void {
        // Logique de génération d'Excel
        console.log("Generating Excel report");
    }
}

class ReportGenerator {
    constructor(private reportFormat: ReportFormat) {}

    generateReport(data: any): void {
        this.reportFormat.generate(data);
    }
}
````
  
</details>

**Conclusion** : Ce principe permet d'ajouter de nouvelles fonctionnalités sans risquer de casser le code existant.

## 3. Liskov Substitution Principle (LSP)

**Concept** : Les objets d'une classe dérivée doivent pouvoir remplacer les objets de la classe de base sans altérer le fonctionnement du programme.

**Exemple concret** :
Si vous avez une classe `Oiseau` et une classe dérivée `Pingouin`, vous ne devriez pas supposer que tous les oiseaux peuvent voler, car un pingouin ne peut pas voler.

**Image mentale** :
*Imaginez une route où différents types de véhicules (voitures, bus, camions) circulent sans problème. Chaque véhicule, bien que différent, peut utiliser la route de la même manière.*

**Exemple détaillé**

Dans cet exemple, la classe ````Penguin```` hérite de ````Bird```` mais ne peut pas voler, ce qui viole le principe LSP. Nous allons utiliser une interface ````Flyable```` pour les oiseaux qui peuvent voler.

<details>
  <summary>Code de l'exemple</summary>

````typescript
class Bird {
    fly(): void {
        console.log("Bird is flying");
    }
}

class Penguin extends Bird {
    fly(): void {
        throw new Error("Penguins can't fly!");
    }
}

>>>> Refactorisé de la manière suivante 

interface Flyable {
    fly(): void;
}

class Bird {}

class Sparrow extends Bird implements Flyable {
    fly(): void {
        console.log("Sparrow is flying");
    }
}

class Penguin extends Bird {}

````
  
</details>

**Conclusion** : Respecter ce principe garantit que les classes dérivées peuvent être utilisées de manière interchangeable avec leurs classes de base.

## 4. Interface Segregation Principle (ISP)

**Concept** : Il vaut mieux avoir plusieurs interfaces spécifiques que de forcer les clients à implémenter une interface générale.

**Exemple concret** :
Au lieu d'avoir une interface `Animal` avec des méthodes `voler()`, `nager()`, et `courir()`, vous devriez avoir des interfaces séparées comme `Volant`, `Nageant`, et `Courant`.

**Image mentale** :
*Une bibliothèque où les livres sont organisés en rayons spécifiques (science-fiction, biographies, romans). Chaque rayon représente une interface spécifique, et vous ne vous attendez pas à trouver un livre de cuisine dans le rayon des romans policiers.* 

**Exemple détaillé**

Dans cet exemple, l'interface ````Worker```` force toutes les classes à implémenter des méthodes qu'elles n'utilisent pas nécessairement. Nous allons séparer les interfaces en ````Workable, Eatable````, et ````Sleepable````

<details>
  <summary>Code de l'exemple</summary>

````typescript
interface Worker {
    work(): void;
    eat(): void;
    sleep(): void;
}

class Human implements Worker {
    work(): void {
        console.log("Human is working");
    }

    eat(): void {
        console.log("Human is eating");
    }

    sleep(): void {
        console.log("Human is sleeping");
    }
}

class Robot implements Worker {
    work(): void {
        console.log("Robot is working");
    }

    eat(): void {
        throw new Error("Robots can't eat!");
    }

    sleep(): void {
        throw new Error("Robots can't sleep!");
    }
}

>>>> Refactorisé de la manière suivante

interface Workable {
    work(): void;
}

interface Eatable {
    eat(): void;
}

interface Sleepable {
    sleep(): void;
}

class Human implements Workable, Eatable, Sleepable {
    work(): void {
        console.log("Human is working");
    }

    eat(): void {
        console.log("Human is eating");
    }

    sleep(): void {
        console.log("Human is sleeping");
    }
}

class Robot implements Workable {
    work(): void {
        console.log("Robot is working");
    }
}

````
  
</details>

**Conclusion** : Ce principe permet de créer des interfaces plus spécifiques et donc plus faciles à implémenter.

## 5. Dependency Inversion Principle (DIP)

**Concept** : Les modules de haut niveau ne doivent pas dépendre des modules de bas niveau, mais des abstractions.

**Exemple concret** :
Au lieu de faire dépendre une classe ````PaymentProcessor```` directement d'une classe ````PayPalService````, elle devrait dépendre d'une interface ````IPaymentService````.

**Image mentale** :
*Une prise électrique où vous pouvez brancher différents appareils (abstractions) sans vous soucier de leur fonctionnement interne (modules de bas niveau).*

**Exemple détaillé**

Dans cet exemple, la classe ````OrderProcessor```` dépend directement de ````EmailService````, ce qui rend difficile le changement du service d'envoi d'emails. Nous allons utiliser une interface ````NotificationService```` pour inverser la dépendance.

<details>
  <summary>Code de l 'exemple</summary>

````typescript
class EmailService {
    send(to: string, message: string): void {
        console.log(`Sending email to ${to}: ${message}`);
    }
}

class OrderProcessor {
    private emailService: EmailService;

    constructor() {
        this.emailService = new EmailService();
    }

    processOrder(orderId: string): void {
        // Logique pour traiter la commande
        this.emailService.send("customer@example.com", "Your order has been processed.");
    }
}

>>>> Refactorisé de la manière suivante

interface NotificationService {
    send(to: string, message: string): void;
}

class EmailService implements NotificationService {
    send(to: string, message: string): void {
        console.log(`Sending email to ${to}: ${message}`);
    }
}

class SMSNotificationService implements NotificationService {
    send(to: string, message: string): void {
        console.log(`Sending SMS to ${to}: ${message}`);
    }
}

class OrderProcessor {
    constructor(private notificationService: NotificationService) {}

    processOrder(orderId: string): void {
        // Logique pour traiter la commande
        this.notificationService.send("customer@example.com", "Your order has been processed.");
    }
}

// Utilisation avec EmailService
const emailService = new EmailService();
const orderProcessorWithEmail = new OrderProcessor(emailService);
orderProcessorWithEmail.processOrder("12345");

// Utilisation avec SMSNotificationService
const smsService = new SMSNotificationService();
const orderProcessorWithSMS = new OrderProcessor(smsService);
orderProcessorWithSMS.processOrder("12345");
````
  
</details>

**Conclusion** : Ce principe réduit les dépendances entre les modules, facilitant ainsi les modifications et les extensions.

---

# Principe KISS : Keep It Simple, Stupid

**Concept** : Les systèmes fonctionnent mieux lorsqu'ils sont simples plutôt que complexes. **La simplicité doit être un objectif clé du design**.

> Attention, suivant les contextes appliquer ce principe à l'extrême peut être contre-productif

**Exemple concret** :
Imaginez que vous devez créer une fonction pour additionner deux nombres. Une approche complexe pourrait impliquer des vérifications inutiles et des optimisations prématurées. Une approche simple serait de simplement écrire `return a + b;`.

**Image mentale** :
*Un crayon à papier. Il est simple, efficace et fait exactement ce pour quoi il est conçu. Pas besoin d'un stylo 4 couleurs pour écrire uniquement en noir...*

**Exemple détaillé**

<details>
  <summary>Code de l'exemple</summary>

````typescript
function isValidEmail(email: string): boolean {
    if (!email) return false;
    const atIndex = email.indexOf('@');
    if (atIndex < 1) return false;
    const dotIndex = email.indexOf('.', atIndex);
    if (dotIndex < atIndex + 2) return false;
    if (dotIndex === email.length - 1) return false;
    return true;
}

>>>> Refactorisé de la manière suivante

function isValidEmail(email: string): boolean {
    const pattern = /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/;
    return pattern.test(email);
}

````

</details>

**Conseils pour appliquer KISS** :
- Évitez les optimisations prématurées.
- Écrivez du code lisible et compréhensible.
- Réduisez la complexité en divisant les problèmes en sous-problèmes plus simples.

---

# Principe DRY (Don't Repeat Yourself)

**Concept** : Chaque morceau de code doit avoir une seule représentation, unitaire, autoritaire et définitive dans le système.

**Exemple concret** :
Si vous avez une fonction qui calcule la TVA dans plusieurs endroits de votre code, vous devriez extraire cette logique dans une fonction unique et l'appeler partout où c'est nécessaire.

**Image mentale** :
*Un livre de recettes où chaque recette est écrite une seule fois. Si vous avez besoin de la recette, vous allez à la page correspondante au lieu de la réécrire.*

**Conseils pour appliquer DRY** :
- Utilisez des fonctions et des méthodes pour encapsuler la logique répétitive.
- Utilisez des constantes pour les valeurs répétées.
- Refactorisez le code pour éliminer les duplications.

# Eviter les abréviations

Bien qu'elles semblent efficace pour réduire la taille du code, elles sont en réalité nocives pour la compréhension du code. Les statistiques montrent qu'un développeur passe plus de temps à lire du code qu'à écrire du code. De ce fait, **l'effort à produire pour faire le mapping mental entre une abréviation et sa signification est plus important que le temps gagné à écrire le code avec des abréviations**. 

Il n'est donc pas recommandé d'utiliser d'abréviation dans le code. Voici un petit exemple pour vous en convaincre :

Remplacer le code suivant : 

````typescript
function sndMsgToUsr(usr: Usr, msg: Msg): void {
	const cfg = getCfg();
	const msg = new MsgSvc(cfg);
	svc.send(msg, usr.id);
}
````

par
````typescript
function sendMessageToUser(user: User, message: Message): void {
	const config = getConfig();
	const messageService = new MessageService(config);
	messageService.send(message, user.id);
}
````

# Pour aller plus loin

[Pour approfondir le sujet, voici une vidéo d'une heure sur les principes du clean code](https://www.youtube.com/watch?v=VioMQpZMtnA&ab_channel=JulienLucas)

## Quelques règles intéressantes

#### Un seul point par ligne
Remplacer le code suivant :

````typescript
const zipCode = user.getAddress().getLocation().getZipCode();
````

par : 

````typescript
const address = user.getAddress();
const location = address.getLocation();
const zipCode = location.getZipCode();
````

#### Conserver les entités les plus petites possibles

Définir une responsabilité claire, éviter les entités "débaras" (ex: service tools, utils qui deviennent des fourre-tout sur le long terme).

On parle souvent de limiter à 100 - 150 lignes maximum par classes / services. 

> **Astuce** : Pour savoir si la taille d'un service / classe / fonction / composant est correcte, se poser la question : **"Est-ce que via un test unitaire, ma fonction, classe, service, composant est testable facilement ?"**

#### Eviter les classes avec plus de deux instances de variables


Remplacer le code suivant : 
````typescript
class OrderProcessor {
	const validator = inject(Validator);
	const calculator = inject(Calculator);
	const emailSender = inject(EmailSender);
	const warehourNotifier = inject(Notifier);
	
	process(order: Order) { ... }
}
````

par 
````typescript
class OrderValidator {
	validate(order: Order): { ... }
}

class OrderNotifier {
	constructor(private emailSender, notifier: Notifier) {}
	
	notify(order: Order) { ... }
}
````

#### principe de First class collection

Ce principe consiste à traiter les collections (listes, ensembles, tableaux etc...) comme des objets à part entière au lieu de les manipuler comme de simples conteneur sur lesquels on applique des boucles, des fonctions externes etc... On préfère ainsi leur attribuer des méthodes qui définissent ce qu'elles peuvent faire

Remplacer le code suivant : 

````typescript
const developers: {name:string, yearsOfExperience: number}[] = [
	{name: 'Dan', yearsOfExperience: 5 },
	{name: 'Lisa', yearsOfExperience: 7 },
	{name: 'Paul', yearsOfExperience: 2 },
]

const isSenior = developers.some(d => d.yearsOfExperience >= 7);	// Cette logique de calcul est en dehors de la collection
````

par : 

````typescript
class Developer {
	constructor(reaonly name: string, readonly yearsOfExperience: number){}
	
	get isSenior(): boolean {
		return this.yearsOfExperience >= 7;
	}
}

class Team {
	constructor(private developers: Developer[]) {}
	
	hasSenior(): boolean {
		return this.developers.some(d => d.isSenior)
	}
}
````

# Rappels sur les conventions de nommage


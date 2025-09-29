[< Retour aux bonnes pratiques - Clean code](https://github.com/gsoulie/Mobile-App-Development/blob/master/resources/clean-code-rules.md)     

# Convention générales de nommage
## Cohérence du langage

Dans un but de cohérence, de compréhension et de transmission du code, les règles suivantes sont préconisées :

* L'anglais doit être utilisé en priorité dans l'écriture du code des applications
  - Cela inclut principalement le code source, les commentaires
* L'utilisation de plusieurs langues au sein d'un même code est proscrite
* Le mix de langue dans le nommage d'un élément est proscrit
  - A ne pas faire : ````getUtilisateur````
  - A ne pas faire : route api de type ````order/commande```` ou ````panier/getCart````

## Choix de la casse
### Règles générales

La casse doit respecter les bonnes pratiques liées à chaque langage

* **CamelCase** : A privilégier pour les nommage de fonctions / paramètres, Typescript, Javascript, Java
ex : ````getUsers, orderTotal````
* **snake_case** : Réservée généralement aux variables et fonctions dans des contextes comme Python, Ruby, etc.
ex : ````user_profile.py, data_loader````
* **PascalCase** : A privilégier pour les noms de classes et d'objets globaux
ex : ````MyComponent, AppConfig````
* **kebab-case** : Utilisée généralement pour les noms de fichiers et d'éléments dans des frameworks front-end
ex : ````my-component.vue, user-profile.css, <my-component/>````
* **SCREAMING_SNAKE_CASE** : A privilégier pour les constantes globales ou valeurs immuables
ex : ````MAX_VALUE, DEFAULT_TIMEOUT````

## Spécificités framework Javascript (Angular, React...)

| Élément                     | Convention         | Exemple                                      |
|-----------------------------|--------------------|----------------------------------------------|
| Type                        | PascalCase         | `export type ProductCategory = {...}`        |
| Interface                   | PascalCase         | `export interface ProductCategory {...}`     |
| Variable                    | camelCase          | `let productId`                              |
| Constante                   | SCREAMING_SNAKE_CASE | `DEFAULT_TIMEOUT`                           |
| Enum                        | PascalCase         | `enum Direction {...}`                       |
| Événement                   | camelCase          | `onClick()`                                  |
| Fonction                    | camelCase          | `fetchProduct()`                             |
| Classe                      | PascalCase         | `class Product {...}`                        |
| Paramètre                   | camelCase          | `getProductDetail(productId: number)`        |
| Nom de fichier              | kebab-case         | `product-detail.ts`, `user-controller.ts`    |
| Nom de composant            | PascalCase         | `ProductList`                                |
| Sélecteur de composant Angular | kebab-case      | `<my-component />`                           |
| Sélecteur de composant React | PascalCase         | `<MyComponent />`                            |
| Route (page ou API)         | lowercase          | `/api/product/[id]`                          |
| Propriété (objet JSON, type, classe, interface...) | camelCase | `let user = { firstName: string, lastName: string }` |


## Longueur des noms

Les noms doivent respecter certaines règles afin de faciliter la compréhension globale du code

* **Explicites mais concis :**
  - Les noms doivent décrire clairement leur intention sans être excessivement longs.
  - Préférer ````user_count````à ````number_of_users_in_the_system````.
* **Pas d'abréviations ambiguës :**
  - Éviter les abréviations non standard ou non évidentes (ex. : ````usrCnt````).
  - Si des abréviations sont utilisées, elles doivent être cohérentes et documentées (ex. : id pour identifier).

## Conventions de nommage par contexte
### Variables
* Utiliser des **noms descriptifs** reflétant leur contenu ou rôle (ex. : ````user, totalAmount````).
* Préférer les **noms singuliers** pour des éléments uniques (ex. : ````user````) et les noms au pluriels pour des collections (ex. : ````users````).
* **Eviter la redondance** d'information en simplifiant les noms (ex: ````orders```` plutôt que ````orderList````)
### Fonctions
* Noms **basés sur des verbes ou actions** (ex. : ````getUser, calculateTotal, renderPage````).
* Doivent indiquer clairement ce que la fonction fait (ex. : ````sendEmail```` au lieu de ````process````).
### Classes
* **Noms au singulier**, reflétant un concept ou un objet (ex. : ````User, Order, PaymentProcessor````).
### Constantes
* **Noms descriptifs** et en SCREAMING_SNAKE_CASE (ex. : ````MAX_RETRIES, API_ENDPOINT````).
### Fichiers
* **Noms descriptifs** en kebab-case ou snake_case, reflétant le contenu ou la fonctionnalité (ex. : ````user-controller.js, data_loader.py````).

## Autres préconisations
* **Pas de noms génériques** : Éviter les noms vagues comme ````data, info, temp ou value```` (ex. : remplacer data par userData).
* **Pas de conventions contradictoires** : Rester cohérent au sein d'un projet ou d'une équipe.
* **Pas de dépendance au contexte local** : Éviter des noms qui ne font sens que pour un lecteur connaissant le contexte spécifique du projet.

# Tutorial de Baeldung
Un tuto qui connecte Spring Boot et Angular. Le tutorial crée une simple application avec un untilisateur à persister dans le backend et à montrer la liste dans le frontend

## Lancement
Pour lancer l'application, lancer Spring Boot en premier et Angular en second. Utiliser l'IDE ou l'invite de commandes dans leurs dossiers respectifs

1. Pour Spring Boot : ```mvn spring-boot:run -Dspring-boot.run.arguments=--spring.main.banner-mode=off,--customArgument=custom```
1. Pour Angular : ```ng serve --open```

## Description
### Partie Spring Boot
La partie Spring Boot est composée d'un POJO entité ```entity```, d'un contrôlleur ```restcontroller```, d'un dépôt ```repository``` et d'une application de lancement.

#### Entity
L'entity est un utilsateur ```User``` qui prend un ID en clé primaire auto-incrémentée, un nom et un E-mail. 

#### RestController
Le ```UserController``` est une classe passant par le Repository pour appliquer les méthodes du CRUD sur les entités de la classe ```User```. 
Elle a pour méthodes

* **GET**, mappée sur ```"/users"```, retourne la liste des utilisateurs
* **POST**, aussi mappée ```"/users"```, fait persister les données du nouvel utilisateur via un formulaire

La classe fait le lien avec la vue sous Angular avec ```@CrossOrigin(origins = "http://localhost:4200")```

#### Repository
Le ```UserRepository``` est une interface qui applique le CRUD sur les instances de l'utilisateur

### Partie Angular

La vue sous Angular affiche les composants du dossier app (```model```, ```service```, ```user-list```, ```user-post```).

#### model
Contient l'objet ```user```, qui prend les mêmes paramètres que le POJO dans le backend du projet

#### service
Fait le lien avec l'application Spring Boot à l'aide d'une injection ```@Injectable()```. 

##### Enregistrement de l'adresse Spring Boot
```
	constructor(private http: HttpClient){
		this.usersUrl = 'http://localhost:8080/users';
	}
  ```
  ##### Définition de la méthode GET
```
	public findAll(): Observable<User[]> {
		return this.http.get<User[]>(this.usersUrl);
	}
  ```
##### Définition de la méthode POST
```
	public save(user: User) {
		return this.http.post<User>(this.usersUrl, user);
	}
```

#### user-list
Le composant lié à la méthode **GET**

#### user-post
Le composant lié à la méthode **POST**

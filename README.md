# Atelier Actif : Introduction aux API avec Laravel

### 🎯 Objectif

À la fin de l’atelier, les étudiants devront être capables de :
- ✅ Comprendre le concept d'API REST et son utilisation dans Laravel.
- ✅ Créer une API simple avec Laravel et y accéder via Postman.
- ✅ Implémenter des routes, contrôleurs et modèles pour gérer une ressource.
- ✅ Collaborer en équipe pour concevoir et tester une API.

### 🕒 Durée : 2h30

### 🔧 Matériel nécessaire
- Un serveur Laravel installé (Laravel 10+ recommandé).
- Postman ou un outil équivalent pour tester l’API.
- Un éditeur de code (VS Code conseillé).
- Base de données MySQL/PostgreSQL (ou SQLite pour simplifier).

---

## 🚀 Déroulement de l’atelier

### 1️⃣ Introduction (15 min) — Enseignant 📢

**Présentation rapide** :
- **Qu’est-ce qu’une API ?**  
  Une API (Application Programming Interface) permet à différents logiciels ou systèmes de communiquer entre eux. Par exemple :
  - **API Météo** : pour obtenir les prévisions météorologiques d’une ville.
  - **API Paiement en ligne** : pour effectuer des paiements via des plateformes comme Stripe ou PayPal.

- **Concepts REST** :
  - **REST** (Representational State Transfer) est un style d’architecture pour concevoir des API.
  - **CRUD** : les opérations de base dans une API REST sont la Création, la Lecture, la Mise à jour, et la Suppression des données.
  - **JSON** : format léger pour échanger des données entre un client et un serveur.

- **Vue d’ensemble d’une API sous Laravel** :  
  Laravel fournit une infrastructure simple pour créer des API avec des routes, des contrôleurs et des modèles.

### 🎯 Mission des groupes :
- Créer une API REST pour gérer une ressource “Produits” avec Laravel.

---

### 2️⃣ Phase d’exploration (20 min) — Travail en équipe 🔍

**Recherche et exploration des éléments clés** :
- **Les routes API dans Laravel** : Comment les définir dans le fichier `routes/api.php` ?
- **Les contrôleurs dans Laravel** : Utilisation de la commande `php artisan make:controller`.
- **Les modèles et migrations dans Laravel** : Création d’un modèle et d’une migration avec `php artisan make:model`.
- **Postman** : Tester l’API avec des requêtes GET, POST, PUT, DELETE.

**Livrable attendu** : Une fiche synthétique collaborative avec les notions clés que chaque groupe aura explorées.

---

### 3️⃣ Mise en pratique (1h15) — Codage en groupe 🖥️

Chaque groupe doit suivre les étapes suivantes :

1️⃣ **Créer un projet Laravel (si ce n’est pas déjà fait)** :
```bash
composer create-project laravel/laravel api-workshop
```

2️⃣ **Créer une migration et un modèle pour la table `products`** :
```bash
php artisan make:model Product -m
```

Dans la migration (`database/migrations/xxxx_xx_xx_create_products_table.php`), ajoutez le code suivant pour créer la table `products` :

```php
public function up()
{
    Schema::create('products', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->text('description')->nullable();
        $table->decimal('price', 8, 2);
        $table->timestamps();
    });
}
```

Ensuite, exécutez la commande suivante pour appliquer la migration et créer la table dans la base de données :
```bash
php artisan migrate
```

3️⃣ **Créer un contrôleur API** :
```bash
php artisan make:controller ProductController --api
```

Dans le contrôleur `ProductController.php`, ajoutez les méthodes suivantes pour gérer les opérations CRUD :

```php
use App\Models\Product;
use Illuminate\Http\Request;

public function index() {
    return Product::all();
}

public function store(Request $request) {
    return Product::create($request->all());
}

public function show(Product $product) {
    return $product;
}

public function update(Request $request, Product $product) {
    $product->update($request->all());
    return $product;
}

public function destroy(Product $product) {
    $product->delete();
    return response()->noContent();
}
```

4️⃣ **Configurer les routes API dans `routes/api.php`** :

Dans le fichier `routes/api.php`, ajoutez la route suivante pour créer automatiquement toutes les routes CRUD :

```php
Route::apiResource('products', ProductController::class);
```

Cela générera les routes suivantes :
- `GET /products` : Liste de tous les produits.
- `POST /products` : Créer un produit.
- `GET /products/{id}` : Afficher un produit spécifique.
- `PUT /products/{id}` : Mettre à jour un produit.
- `DELETE /products/{id}` : Supprimer un produit.

5️⃣ **Tester avec Postman** :  
Chaque groupe doit tester les différentes routes API avec Postman en effectuant des requêtes :
- **GET** : pour récupérer tous les produits ou un produit spécifique.
- **POST** : pour créer un nouveau produit.
- **PUT** : pour mettre à jour un produit.
- **DELETE** : pour supprimer un produit.

### 🚨 Bonnes pratiques :
- Vérifier que les réponses des API sont au format JSON.
- Tester les différentes méthodes HTTP (GET, POST, PUT, DELETE).
- Utiliser des assertions dans Postman pour vérifier les réponses attendues (codes HTTP, contenu, etc.).

---

### 📚 Conclusion (10 min) — Discussion et questions 🧠

- Récapitulation des concepts et techniques utilisés pendant l'atelier.
- Questions ouvertes : difficultés rencontrées, suggestions d'amélioration, et pistes pour aller plus loin (authentification, pagination, validation des données).

---

### 🌟 Références
- [Laravel Documentation](https://laravel.com/docs)
- [Postman Documentation](https://learning.postman.com/docs/)
- [RESTful API Design](https://restfulapi.net/)

---

# Films & Séries TV

Architecture microservices Node.js avec REST, GraphQL et gRPC.

---

##  Architecture

```
Client
  │
  ▼
API Gateway (Express — port 3000)
  ├── REST  → /movies, /movies/:id, /tvshows, /tvshows/:id
  └── GraphQL → /graphql
        │
        ├── gRPC ──► Movie Microservice (port 50051)
        └── gRPC ──► TVShow Microservice (port 50052)
```

---

##  Structure du projet

```
microservices avec ret graphql et grpc/  
└── tests
```

---

##  Prérequis

- [Node.js](https://nodejs.org/) v18+
- npm

---

##  Installation

```bash
# 1. Créer et accéder au répertoire
mkdir tp-microservices && cd tp-microservices

# 2. Initialiser le projet
npm init -y

# 3. Installer les dépendances
npm install express @apollo/server graphql @as-integrations/express4 \
  @grpc/grpc-js @grpc/proto-loader cors
```

---

##  Démarrage

Ouvrir **trois terminaux séparés** et lancer dans cet ordre :

```bash
# Terminal 1 — Microservice Films
node movieMicroservice.js

# Terminal 2 — Microservice Séries TV
node tvShowMicroservice.js

# Terminal 3 — API Gateway
node apiGateway.js
```

---

##  Tests

### REST

```bash
# Liste des films
GET http://localhost:3000/movies

# Film par ID
GET http://localhost:3000/movies/1

# Liste des séries TV
GET http://localhost:3000/tvshows

# Série TV par ID
GET http://localhost:3000/tvshows/1
```

### GraphQL

Accéder à l'explorateur : `http://localhost:3000/graphql`

```graphql
# Tous les films
query {
  movies {
    id
    title
    description
  }
}

# Un film par ID
query {
  movie(id: "1") {
    id
    title
    description
  }
}

# Toutes les séries TV
query {
  tvShows {
    id
    title
    description
  }
}

# Une série TV par ID
query {
  tvShow(id: "1") {
    id
    title
    description
  }
}
```

---

##  Ports

| Service              | Port  | Protocole |
|----------------------|-------|-----------|
| API Gateway          | 3000  | HTTP      |
| Movie Microservice   | 50051 | gRPC      |
| TVShow Microservice  | 50052 | gRPC      |

---

##  Extensions prévues

- [ ] Opérations CRUD (création, mise à jour, suppression) via REST, GraphQL et gRPC
- [ ] Connexion à une base de données (MongoDB / PostgreSQL)
- [ ] Intégration Kafka pour la communication asynchrone

---

##  Dépendances

| Package                    | Rôle                              |
|----------------------------|-----------------------------------|
| `express`                  | Serveur HTTP / API Gateway        |
| `@apollo/server`           | Serveur GraphQL                   |
| `graphql`                  | Moteur GraphQL                    |
| `@as-integrations/express4`| Intégration Apollo + Express      |
| `@grpc/grpc-js`            | Client/Serveur gRPC               |
| `@grpc/proto-loader`       | Chargement des fichiers `.proto`  |
| `cors`                     | Gestion des requêtes cross-origin |

---


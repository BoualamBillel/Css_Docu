# Guide Complet des Bibliothèques CSS

## Table des Matières
1. [Introduction](#introduction)
2. [Bootstrap](#bootstrap)
3. [Tailwind CSS](#tailwind-css)
4. [Material-UI (MUI)](#material-ui)
5. [Bulma](#bulma)
6. [Foundation](#foundation)
7. [Semantic UI](#semantic-ui)
8. [Comparaison et Choix](#comparaison)

---

## Introduction

Les bibliothèques CSS sont des frameworks qui fournissent des composants pré-stylisés et des utilitaires pour accélérer le développement web. Ce guide détaille les bibliothèques les plus populaires, leur utilisation, et leur intégration avec Angular et React.

---

## Bootstrap

### Qu'est-ce que Bootstrap ?
Bootstrap est le framework CSS le plus populaire au monde, créé par Twitter. Il fournit un système de grille responsive et des composants UI pré-conçus.

### Quand l'utiliser ?
- Projets nécessitant un développement rapide
- Applications d'entreprise avec des interfaces standard
- Sites web responsive avec design cohérent
- Prototypes et MVP

### Pourquoi l'utiliser ?
- **Popularité** : Grande communauté et nombreuses ressources
- **Composants riches** : Navbar, modals, cards, boutons, formulaires
- **Grid système** : Système de grille flexible en 12 colonnes
- **Documentation** : Documentation excellente et complète
- **Compatibilité** : Fonctionne sur tous les navigateurs modernes

### Installation et Intégration

#### Avec React

**Installation:**
```bash
npm install bootstrap react-bootstrap
```

**Exemple de composant Card:**
```jsx
import React from 'react';
import { Card, Button } from 'react-bootstrap';
import 'bootstrap/dist/css/bootstrap.min.css';

function ProductCard() {
  return (
    <Card style={{ width: '18rem' }}>
      <Card.Img variant="top" src="product.jpg" />
      <Card.Body>
        <Card.Title>Nom du Produit</Card.Title>
        <Card.Text>
          Description détaillée du produit avec toutes les informations
          importantes pour l'utilisateur.
        </Card.Text>
        <Button variant="primary">Acheter</Button>
      </Card.Body>
    </Card>
  );
}

export default ProductCard;
```

**Effet du code:**
- `Card` crée un conteneur avec bordures arrondies et ombre
- `Card.Img` affiche l'image avec bordures supérieures arrondies
- `Card.Body` ajoute du padding autour du contenu
- `Button variant="primary"` applique la couleur primaire (bleu par défaut)

**Exemple de Grid System:**
```jsx
import { Container, Row, Col } from 'react-bootstrap';

function ResponsiveGrid() {
  return (
    <Container>
      <Row>
        <Col xs={12} md={6} lg={4}>
          <div className="p-3 bg-light border">Colonne 1</div>
        </Col>
        <Col xs={12} md={6} lg={4}>
          <div className="p-3 bg-light border">Colonne 2</div>
        </Col>
        <Col xs={12} md={12} lg={4}>
          <div className="p-3 bg-light border">Colonne 3</div>
        </Col>
      </Row>
    </Container>
  );
}
```

**Effet du code:**
- Sur mobile (xs): 3 colonnes empilées verticalement (12/12)
- Sur tablette (md): 2 colonnes de 50% + 1 pleine largeur
- Sur desktop (lg): 3 colonnes égales de 33.33%

#### Avec Angular

**Installation:**
```bash
npm install bootstrap @ng-bootstrap/ng-bootstrap
```

**Configuration dans angular.json:**
```json
"styles": [
  "node_modules/bootstrap/dist/css/bootstrap.min.css",
  "src/styles.css"
]
```

**Exemple de Modal:**
```typescript
// app.component.ts
import { Component } from '@angular/core';
import { NgbModal } from '@ng-bootstrap/ng-bootstrap';

@Component({
  selector: 'app-root',
  template: `
    <button class="btn btn-primary" (click)="open(content)">
      Ouvrir Modal
    </button>

    <ng-template #content let-modal>
      <div class="modal-header">
        <h4 class="modal-title">Titre du Modal</h4>
        <button type="button" class="btn-close" 
                (click)="modal.dismiss()"></button>
      </div>
      <div class="modal-body">
        <p>Contenu du modal avec des informations importantes.</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" 
                (click)="modal.close()">Fermer</button>
        <button type="button" class="btn btn-primary">
          Sauvegarder
        </button>
      </div>
    </ng-template>
  `
})
export class AppComponent {
  constructor(private modalService: NgbModal) {}

  open(content: any) {
    this.modalService.open(content);
  }
}
```

**Effet du code:**
- Le bouton ouvre une fenêtre modale centrée avec un overlay sombre
- `modal-header` affiche le titre avec bouton de fermeture
- `modal-body` contient le contenu principal
- `modal-footer` propose les actions (boutons alignés à droite)

---

## Tailwind CSS

### Qu'est-ce que Tailwind CSS ?
Tailwind est un framework CSS "utility-first" qui fournit des classes utilitaires de bas niveau pour construire des designs personnalisés.

### Quand l'utiliser ?
- Projets nécessitant un design unique et personnalisé
- Équipes qui veulent contrôle total sur le style
- Applications modernes avec design systems
- Projets où la taille du bundle CSS est importante

### Pourquoi l'utiliser ?
- **Flexibilité** : Création de designs uniques sans CSS personnalisé
- **Performance** : PurgeCSS supprime CSS non utilisé
- **Productivité** : Pas besoin de nommer les classes
- **Responsive** : Modificateurs responsive intégrés
- **Dark mode** : Support natif du mode sombre

### Installation et Intégration

#### Avec React

**Installation:**
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

**Configuration tailwind.config.js:**
```javascript
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        'brand': '#ff6b6b',
      }
    },
  },
  plugins: [],
}
```

**Exemple de Card moderne:**
```jsx
function ModernCard() {
  return (
    <div className="max-w-sm rounded-lg overflow-hidden shadow-lg 
                    hover:shadow-2xl transition-shadow duration-300 
                    bg-white">
      <img 
        className="w-full h-48 object-cover" 
        src="image.jpg" 
        alt="Product"
      />
      <div className="px-6 py-4">
        <h2 className="font-bold text-xl mb-2 text-gray-800">
          Titre du Produit
        </h2>
        <p className="text-gray-600 text-base leading-relaxed">
          Description détaillée avec toutes les informations importantes
          pour l'utilisateur.
        </p>
      </div>
      <div className="px-6 pb-4">
        <button className="bg-blue-500 hover:bg-blue-700 text-white 
                         font-bold py-2 px-4 rounded-full 
                         transition-colors duration-200">
          Acheter
        </button>
      </div>
    </div>
  );
}
```

**Effet du code:**
- `max-w-sm` : largeur maximale small (384px)
- `rounded-lg` : bordures arrondies larges (8px)
- `shadow-lg` : ombre large, `hover:shadow-2xl` : ombre plus grande au survol
- `transition-shadow duration-300` : animation fluide de 300ms
- `object-cover` : image couvre la zone en conservant proportions
- `text-gray-800` : texte gris foncé pour le titre
- `leading-relaxed` : hauteur de ligne augmentée pour meilleure lisibilité

**Exemple Responsive:**
```jsx
function ResponsiveLayout() {
  return (
    <div className="container mx-auto px-4">
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div className="bg-blue-100 p-6 rounded-lg">
          <h3 className="text-lg font-semibold mb-3">Feature 1</h3>
          <p className="text-sm text-gray-700">Description</p>
        </div>
        <div className="bg-green-100 p-6 rounded-lg">
          <h3 className="text-lg font-semibold mb-3">Feature 2</h3>
          <p className="text-sm text-gray-700">Description</p>
        </div>
        <div className="bg-purple-100 p-6 rounded-lg">
          <h3 className="text-lg font-semibold mb-3">Feature 3</h3>
          <p className="text-sm text-gray-700">Description</p>
        </div>
      </div>
    </div>
  );
}
```

**Effet du code:**
- Mobile : 1 colonne (grid-cols-1)
- Tablette (md) : 2 colonnes (md:grid-cols-2)
- Desktop (lg) : 3 colonnes (lg:grid-cols-3)
- `gap-6` : espacement de 1.5rem entre les éléments

#### Avec Angular

**Installation:**
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

**Configuration dans angular.json:**
```json
"styles": [
  "src/styles.css"
],
"scripts": []
```

**styles.css:**
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

**Exemple de Formulaire:**
```typescript
@Component({
  selector: 'app-contact-form',
  template: `
    <form class="max-w-md mx-auto mt-8 bg-white p-8 rounded-xl shadow-lg">
      <h2 class="text-2xl font-bold mb-6 text-gray-800">
        Contactez-nous
      </h2>
      
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2">
          Nom
        </label>
        <input 
          type="text"
          class="w-full px-3 py-2 border border-gray-300 rounded-lg 
                 focus:outline-none focus:ring-2 focus:ring-blue-500 
                 focus:border-transparent transition-all"
          placeholder="Votre nom"
        />
      </div>

      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2">
          Email
        </label>
        <input 
          type="email"
          class="w-full px-3 py-2 border border-gray-300 rounded-lg 
                 focus:outline-none focus:ring-2 focus:ring-blue-500 
                 focus:border-transparent transition-all"
          placeholder="votre@email.com"
        />
      </div>

      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-bold mb-2">
          Message
        </label>
        <textarea 
          class="w-full px-3 py-2 border border-gray-300 rounded-lg 
                 focus:outline-none focus:ring-2 focus:ring-blue-500 
                 focus:border-transparent transition-all h-32 resize-none"
          placeholder="Votre message"
        ></textarea>
      </div>

      <button 
        type="submit"
        class="w-full bg-blue-500 hover:bg-blue-600 text-white 
               font-bold py-3 px-4 rounded-lg transition-colors 
               duration-200 transform hover:scale-105">
        Envoyer
      </button>
    </form>
  `
})
export class ContactFormComponent {}
```

**Effet du code:**
- `focus:ring-2` : anneau bleu de 2px apparaît au focus
- `focus:border-transparent` : bordure devient transparente au focus
- `transition-all` : anime tous les changements
- `hover:scale-105` : agrandit légèrement le bouton au survol (105%)
- `resize-none` : empêche le redimensionnement du textarea

---

## Material-UI (MUI)

### Qu'est-ce que Material-UI ?
Material-UI est une bibliothèque de composants React implémentant les directives Material Design de Google.

### Quand l'utiliser ?
- Applications React avec design Material
- Projets nécessitant composants complexes (DataGrid, Autocomplete)
- Applications d'entreprise professionnelles
- Équipes qui apprécient Material Design

### Pourquoi l'utiliser ?
- **Composants riches** : Bibliothèque très complète
- **Thématisation** : Système de thème puissant
- **Accessibilité** : Composants accessibles par défaut
- **TypeScript** : Support TypeScript excellent
- **Écosystème** : Outils additionnels (MUI X pour DataGrid)

### Installation et Intégration avec React

**Installation:**
```bash
npm install @mui/material @emotion/react @emotion/styled
npm install @mui/icons-material
```

**Exemple de Dashboard:**
```jsx
import React from 'react';
import {
  AppBar, Toolbar, Typography, Button, Card, CardContent,
  CardActions, Grid, Container, IconButton
} from '@mui/material';
import { Menu as MenuIcon, Favorite, Share } from '@mui/icons-material';

function Dashboard() {
  return (
    <>
      <AppBar position="static">
        <Toolbar>
          <IconButton edge="start" color="inherit" sx={{ mr: 2 }}>
            <MenuIcon />
          </IconButton>
          <Typography variant="h6" sx={{ flexGrow: 1 }}>
            Mon Application
          </Typography>
          <Button color="inherit">Connexion</Button>
        </Toolbar>
      </AppBar>

      <Container sx={{ mt: 4 }}>
        <Grid container spacing={3}>
          <Grid item xs={12} md={6} lg={4}>
            <Card elevation={3}>
              <CardContent>
                <Typography variant="h5" component="div" gutterBottom>
                  Carte 1
                </Typography>
                <Typography variant="body2" color="text.secondary">
                  Contenu de la carte avec des informations détaillées
                  sur le produit ou service.
                </Typography>
              </CardContent>
              <CardActions>
                <IconButton aria-label="ajouter aux favoris">
                  <Favorite />
                </IconButton>
                <IconButton aria-label="partager">
                  <Share />
                </IconButton>
                <Button size="small">En savoir plus</Button>
              </CardActions>
            </Card>
          </Grid>

          <Grid item xs={12} md={6} lg={4}>
            <Card elevation={3}>
              <CardContent>
                <Typography variant="h5" component="div" gutterBottom>
                  Carte 2
                </Typography>
                <Typography variant="body2" color="text.secondary">
                  Une autre carte avec du contenu différent mais
                  le même style cohérent.
                </Typography>
              </CardContent>
              <CardActions>
                <IconButton aria-label="ajouter aux favoris">
                  <Favorite />
                </IconButton>
                <IconButton aria-label="partager">
                  <Share />
                </IconButton>
                <Button size="small">En savoir plus</Button>
              </CardActions>
            </Card>
          </Grid>
        </Grid>
      </Container>
    </>
  );
}

export default Dashboard;
```

**Effet du code:**
- `AppBar` : barre d'en-tête fixe avec couleur primaire
- `elevation={3}` : ombre de profondeur 3 (Material Design)
- `sx={{ mt: 4 }}` : margin-top de 32px (4 * 8px)
- `variant="h5"` : typographie h5 avec styles Material prédéfinis
- `gutterBottom` : ajoute marge inférieure au texte
- `color="text.secondary"` : couleur de texte secondaire (gris)

**Exemple de Formulaire avec validation:**
```jsx
import React, { useState } from 'react';
import {
  TextField, Button, Box, Alert, CircularProgress
} from '@mui/material';

function LoginForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();
    setLoading(true);
    setError('');
    
    // Simulation d'appel API
    setTimeout(() => {
      if (email && password) {
        setError('');
        console.log('Connexion réussie');
      } else {
        setError('Email et mot de passe requis');
      }
      setLoading(false);
    }, 2000);
  };

  return (
    <Box
      component="form"
      onSubmit={handleSubmit}
      sx={{
        maxWidth: 400,
        mx: 'auto',
        mt: 8,
        p: 3,
        boxShadow: 3,
        borderRadius: 2
      }}
    >
      <Typography variant="h4" align="center" gutterBottom>
        Connexion
      </Typography>

      {error && (
        <Alert severity="error" sx={{ mb: 2 }}>
          {error}
        </Alert>
      )}

      <TextField
        fullWidth
        label="Email"
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        margin="normal"
        required
        variant="outlined"
      />

      <TextField
        fullWidth
        label="Mot de passe"
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        margin="normal"
        required
        variant="outlined"
      />

      <Button
        type="submit"
        fullWidth
        variant="contained"
        size="large"
        disabled={loading}
        sx={{ mt: 3 }}
      >
        {loading ? <CircularProgress size={24} /> : 'Se connecter'}
      </Button>
    </Box>
  );
}
```

**Effet du code:**
- `TextField` : input avec animation du label (flotte vers le haut)
- `variant="outlined"` : bordure visible autour du champ
- `Alert severity="error"` : bannière rouge avec icône d'erreur
- `CircularProgress` : spinner animé pendant le chargement
- `disabled={loading}` : désactive le bouton pendant chargement
- `boxShadow: 3` : ombre MUI niveau 3

---

## Bulma

### Qu'est-ce que Bulma ?
Bulma est un framework CSS moderne basé sur Flexbox, sans JavaScript.

### Quand l'utiliser ?
- Projets nécessitant uniquement CSS (pas de JS)
- Sites statiques ou applications simples
- Développeurs préférant Flexbox à Grid
- Projets nécessitant un framework léger

### Pourquoi l'utiliser ?
- **Pure CSS** : Aucun JavaScript requis
- **Moderne** : Basé entièrement sur Flexbox
- **Modulaire** : Importez uniquement ce dont vous avez besoin
- **Lisible** : Noms de classes intuitifs
- **Léger** : Plus petit que Bootstrap

### Installation et Intégration

#### Avec React

**Installation:**
```bash
npm install bulma
```

**Importation:**
```jsx
import 'bulma/css/bulma.min.css';

function HeroSection() {
  return (
    <section className="hero is-primary is-medium">
      <div className="hero-body">
        <div className="container">
          <h1 className="title is-1">
            Titre Principal
          </h1>
          <h2 className="subtitle is-3">
            Sous-titre avec description du service ou produit
          </h2>
          <button className="button is-large is-light">
            Commencer
          </button>
        </div>
      </div>
    </section>
  );
}
```

**Effet du code:**
- `hero is-primary` : section hero avec couleur primaire (turquoise)
- `is-medium` : hauteur moyenne (taille pré-définie)
- `title is-1` : titre de taille 1 (3rem)
- `button is-large is-light` : grand bouton avec couleur claire

**Exemple de Grid:**
```jsx
function ProductGrid() {
  return (
    <div className="container">
      <div className="columns is-multiline">
        <div className="column is-one-third">
          <div className="box">
            <article className="media">
              <div className="media-left">
                <figure className="image is-64x64">
                  <img src="icon1.png" alt="Icon" />
                </figure>
              </div>
              <div className="media-content">
                <div className="content">
                  <p>
                    <strong>Feature 1</strong>
                    <br />
                    Description de la fonctionnalité principale
                  </p>
                </div>
              </div>
            </article>
          </div>
        </div>

        <div className="column is-one-third">
          <div className="box">
            <article className="media">
              <div className="media-left">
                <figure className="image is-64x64">
                  <img src="icon2.png" alt="Icon" />
                </figure>
              </div>
              <div className="media-content">
                <div className="content">
                  <p>
                    <strong>Feature 2</strong>
                    <br />
                    Description de la fonctionnalité secondaire
                  </p>
                </div>
              </div>
            </article>
          </div>
        </div>

        <div className="column is-one-third">
          <div className="box">
            <article className="media">
              <div className="media-left">
                <figure className="image is-64x64">
                  <img src="icon3.png" alt="Icon" />
                </figure>
              </div>
              <div className="media-content">
                <div className="content">
                  <p>
                    <strong>Feature 3</strong>
                    <br />
                    Description de la fonctionnalité tertiaire
                  </p>
                </div>
              </div>
            </article>
          </div>
        </div>
      </div>
    </div>
  );
}
```

**Effet du code:**
- `columns` : conteneur flex pour les colonnes
- `is-multiline` : permet aux colonnes de passer à la ligne
- `is-one-third` : colonne de 33.33% de largeur
- `box` : conteneur avec padding, bordure et ombre
- `media` : composant pour contenu avec image + texte
- `image is-64x64` : image carrée de 64x64px

#### Avec Angular

**Installation et configuration:**
```bash
npm install bulma
```

**angular.json:**
```json
"styles": [
  "node_modules/bulma/css/bulma.min.css",
  "src/styles.css"
]
```

**Exemple de Navbar:**
```typescript
@Component({
  selector: 'app-navbar',
  template: `
    <nav class="navbar is-dark" role="navigation">
      <div class="navbar-brand">
        <a class="navbar-item" href="#">
          <img src="logo.png" alt="Logo">
        </a>

        <a role="button" 
           class="navbar-burger" 
           [class.is-active]="isActive"
           (click)="toggleMenu()">
          <span></span>
          <span></span>
          <span></span>
        </a>
      </div>

      <div class="navbar-menu" [class.is-active]="isActive">
        <div class="navbar-start">
          <a class="navbar-item">Accueil</a>
          <a class="navbar-item">Produits</a>
          <a class="navbar-item">Contact</a>
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a class="button is-primary">
                <strong>S'inscrire</strong>
              </a>
              <a class="button is-light">
                Connexion
              </a>
            </div>
          </div>
        </div>
      </div>
    </nav>
  `
})
export class NavbarComponent {
  isActive = false;

  toggleMenu() {
    this.isActive = !this.isActive;
  }
}
```

**Effet du code:**
- `navbar is-dark` : barre de navigation sombre
- `navbar-burger` : icône hamburger pour mobile
- `is-active` : classe qui affiche/masque le menu mobile
- `navbar-start` : éléments alignés à gauche
- `navbar-end` : éléments alignés à droite
- Responsive automatique avec breakpoint à 1024px

---

## Foundation

### Qu'est-ce que Foundation ?
Foundation est un framework CSS responsive professionnel créé par ZURB, utilisé par de grandes entreprises.

### Quand l'utiliser ?
- Projets d'entreprise complexes
- Sites nécessitant accessibilité avancée
- Applications avec grille complexe
- Projets email responsive

### Pourquoi l'utiliser ?
- **Professionnel** : Utilisé par Facebook, eBay, Mozilla
- **Accessibilité** : Excellent support ARIA
- **Flexible** : Très personnalisable avec Sass
- **Email** : Framework pour emails responsive
- **Mobile-first** : Conçu mobile-first

### Installation avec React

**Installation:**
```bash
npm install foundation-sites
```

**Exemple de Grid:**
```jsx
import 'foundation-sites/dist/css/foundation.min.css';

function FoundationGrid() {
  return (
    <div className="grid-container">
      <div className="grid-x grid-margin-x">
        <div className="cell small-12 medium-6 large-4">
          <div className="callout">
            <h3>Section 1</h3>
            <p>Contenu de la première section avec informations.</p>
          </div>
        </div>
        <div className="cell small-12 medium-6 large-4">
          <div className="callout">
            <h3>Section 2</h3>
            <p>Contenu de la deuxième section avec détails.</p>
          </div>
        </div>
        <div className="cell small-12 medium-12 large-4">
          <div className="callout">
            <h3>Section 3</h3>
            <p>Contenu de la troisième section avec exemples.</p>
          </div>
        </div>
      </div>
    </div>
  );
}
```

**Effet du code:**
- `grid-container` : conteneur avec max-width
- `grid-x` : conteneur flex horizontal
- `grid-margin-x` : marges horizontales entre cellules
- `cell` : cellule de grille flex
- `small-12` : 100% sur mobile
- `medium-6` : 50% sur tablette
- `large-4` : 33.33% sur desktop

---

## Semantic UI

### Qu'est-ce que Semantic UI ?
Framework CSS avec convention de nommage en langage naturel, rendant le code très lisible.

### Quand l'utiliser ?
- Projets nécessitant code très lisible
- Équipes avec designers et développeurs
- Applications avec nombreux composants UI
- Prototypes rapides

### Pourquoi l'utiliser ?
- **Lisibilité** : Classes en anglais naturel
- **Thèmes** : Système de thèmes puissant
- **Composants** : Large bibliothèque de composants
- **Intégrations** : Support React officiel

### Installation avec React

**Installation:**
```bash
npm install semantic-ui-react semantic-ui-css
```

**Exemple:**
```jsx
import 'semantic-ui-css/semantic.min.css';
import { Button, Card, Icon, Image } from 'semantic-ui-react';

function SemanticCard() {
  return (
    <Card>
      <Image src='product.jpg' wrapped ui={false} />
      <Card.Content>
        <Card.Header>Nom du Produit</Card.Header>
        <Card.Meta>
          <span className='date'>Ajouté en 2024</span>
        </Card.Meta>
        <Card.Description>
          Description détaillée du produit avec toutes les
          caractéristiques importantes.
        </Card.Description>
      </Card.Content>
      <Card.Content extra>
        <Button primary>
          <Icon name='shop' />
          Acheter
        </Button>
        <Button>
          <Icon name='heart' />
          Favoris
        </Button>
      </Card.Content>
    </Card>
  );
}
```

**Effet du code:**
- `Card` : conteneur avec bordure et ombre subtile
- `wrapped ui={false}` : image sans padding supplémentaire
- `Card.Header` : titre en gras, plus grand
- `Card.Meta` : métadonnées en gris clair
- `primary` : bouton bleu avec effet hover

---

## Comparaison et Choix

### Tableau Comparatif

| Framework | Taille | Courbe d'apprentissage | Personnalisation | Meilleur pour |
|-----------|--------|----------------------|------------------|---------------|
| Bootstrap | ~200KB | Facile | Moyenne | Prototypes rapides, apps standard |
| Tailwind | Variable | Moyenne | Élevée | Designs personnalisés, apps modernes |
| Material-UI | ~300KB | Moyenne | Élevée | Apps React Material Design |
| Bulma | ~200KB | Facile | Moyenne | Sites simples, pure CSS |
| Foundation | ~150KB | Difficile | Élevée | Projets entreprise complexes |
| Semantic UI | ~250KB | Facile | Moyenne | Code lisible, prototypes |

### Critères de Choix

**Choisissez Bootstrap si:**
- Vous voulez démarrer rapidement
- Vous avez besoin de composants standards
- Votre équipe connaît déjà Bootstrap
- Vous construisez un MVP ou prototype

**Choisissez Tailwind si:**
- Vous voulez un design unique
- Vous aimez l'approche utility-first
- La performance est critique
- Vous ne voulez pas écrire de CSS personnalisé

**Choisissez Material-UI si:**
- Vous développez en React
- Vous aimez Material Design
- Vous avez besoin de composants complexes
- L'accessibilité est importante

**Choisissez Bulma si:**
- Vous ne voulez pas de JavaScript
- Vous préférez Flexbox
- Vous voulez un framework léger
- Vous aimez la syntaxe simple

**Choisissez Foundation si:**
- Vous travaillez sur un projet entreprise
- L'accessibilité est critique
- Vous avez besoin de grilles complexes
- Vous développez des emails responsive

**Choisissez Semantic UI si:**
- Vous voulez un code très lisible
- Vous travaillez en équipe mixte
- Vous aimez les noms de classes naturels
- Vous développez en React

### Bonnes Pratiques Générales

1. **Ne mélangez pas les frameworks** : Utilisez un seul framework par projet
2. **Personnalisez avec parcimonie** : Évitez de surcharger avec du CSS custom
3. **Optimisez la production** : Utilisez PurgeCSS ou tree-shaking
4. **Restez cohérent** : Suivez les conventions du framework
5. **Testez la performance** : Mesurez l'impact sur le temps de chargement
6. **Considérez l'accessibilité** : Utilisez les composants accessibles
7. **Documentez** : Expliquez pourquoi vous avez choisi tel framework

---

## Conclusion

Chaque bibliothèque CSS a ses forces et faiblesses. Le choix dépend de :
- Vos besoins projet (rapidité vs personnalisation)
- Votre stack technique (React, Angular, Vue)
- Vos compétences équipe
- Vos contraintes performance
- Votre design system

Les frameworks évoluent constamment. Restez à jour avec leur documentation officielle et leur communauté.

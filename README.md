# 🛍️ Hichoux Store

> Système E-Commerce complet pour le Maroc avec gestion des commandes, confirmation téléphonique, et intégration sociétés de livraison.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Supabase](https://img.shields.io/badge/database-Supabase-3ECF8E)

---

## 📸 Screenshots

| Frontend | Admin Dashboard |
|----------|-----------------|
| ![Frontend](docs/screenshots/frontend.png) | ![Admin](docs/screenshots/admin.png) |

---

## ✨ Fonctionnalités

### 🛒 Frontend Client
- Catalogue produits avec filtres
- Panier persistant (localStorage)
- Checkout avec paiement à la livraison (COD)
- Suivi de commande en temps réel
- Design responsive et moderne

### ⚙️ Backend Admin
- Dashboard avec statistiques temps réel
- Gestion des commandes (Kanban)
- Module de confirmation (Appel/WhatsApp)
- Création de bordereaux d'expédition
- Gestion des produits et stock
- Synchronisation Google Sheets
- Intégration API Digylog

### 🗄️ Base de Données
- Supabase (PostgreSQL)
- Row Level Security (RLS)
- Triggers automatiques
- Temps réel activé

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     FRONTEND CLIENT                          │
│              /frontend/index.html                            │
│         Catalogue • Panier • Checkout • Suivi                │
└─────────────────────────────────────────────────────────────┘
                              │
                              │ API REST + Realtime
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                        SUPABASE                              │
│                                                              │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐        │
│  │ Products│  │ Orders  │  │Customers│  │Shipments│        │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘        │
│                                                              │
│         Auth • Storage • Realtime • Edge Functions          │
└─────────────────────────────────────────────────────────────┘
                              │
                              │ API REST + Realtime
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      BACKEND ADMIN                           │
│               /admin/index.html                              │
│    Dashboard • Commandes • Confirmation • Expédition         │
└─────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
        ┌──────────┐   ┌──────────┐   ┌──────────┐
        │  Google  │   │  Digylog │   │  Ozone   │
        │  Sheets  │   │   API    │   │   API    │
        └──────────┘   └──────────┘   └──────────┘
```

---

## 📁 Structure du Projet

```
hichoux-store/
├── 📄 README.md                 # Documentation
├── 📄 .gitignore               # Fichiers à ignorer
├── 📄 .env.example             # Template variables d'environnement
│
├── 📁 config/
│   └── config.js               # Configuration centralisée
│
├── 📁 database/
│   ├── schema.sql              # Schema complet Supabase
│   └── seed.sql                # Données d'exemple
│
├── 📁 frontend/                # Site client
│   ├── index.html              # Page principale
│   ├── 📁 css/
│   │   └── style.css           # Styles frontend
│   ├── 📁 js/
│   │   ├── config.js           # Config frontend
│   │   ├── supabase.js         # Client Supabase
│   │   ├── app.js              # Logic principale
│   │   ├── products.js         # Gestion produits
│   │   ├── cart.js             # Gestion panier
│   │   └── checkout.js         # Gestion commande
│   └── 📁 assets/
│       └── images/             # Images statiques
│
├── 📁 admin/                   # Dashboard admin
│   ├── index.html              # Page admin
│   ├── 📁 css/
│   │   └── admin.css           # Styles admin
│   └── 📁 js/
│       ├── config.js           # Config admin
│       ├── supabase.js         # Client Supabase
│       ├── app.js              # Logic principale
│       ├── dashboard.js        # Module dashboard
│       ├── orders.js           # Module commandes
│       ├── confirmation.js     # Module confirmation
│       ├── shipping.js         # Module expédition
│       └── products.js         # Module produits
│
├── 📁 scripts/
│   └── google-apps-script.js   # Script Google Sheets
│
└── 📁 docs/
    ├── INSTALLATION.md         # Guide d'installation
    ├── API.md                  # Documentation API
    └── 📁 screenshots/         # Captures d'écran
```

---

## 🚀 Installation Rapide

### Prérequis
- Un compte [Supabase](https://supabase.com) (gratuit)
- Un compte [Google](https://google.com) pour Google Sheets
- (Optionnel) Un compte [Digylog](https://digylog.com)

### 1. Cloner le projet

```bash
git clone https://github.com/votre-username/hichoux-store.git
cd hichoux-store
```

### 2. Configurer Supabase

1. Créer un nouveau projet sur [supabase.com](https://supabase.com)
2. Aller dans **SQL Editor** → **New Query**
3. Copier/coller le contenu de `database/schema.sql`
4. Exécuter le script
5. Noter l'**URL** et l'**anon key** depuis **Settings → API**

### 3. Configurer les fichiers

Copier `.env.example` vers `.env` et remplir :

```env
SUPABASE_URL=https://votre-projet.supabase.co
SUPABASE_ANON_KEY=votre-anon-key
GOOGLE_SCRIPT_URL=https://script.google.com/macros/s/xxx/exec
DIGYLOG_API_TOKEN=votre-token-digylog
```

Puis mettre à jour `config/config.js` avec vos valeurs.

### 4. Lancer localement

Option A - Avec Live Server (VS Code) :
1. Installer l'extension "Live Server"
2. Clic droit sur `frontend/index.html` → "Open with Live Server"

Option B - Avec Python :
```bash
python -m http.server 8000
# Ouvrir http://localhost:8000/frontend/
```

Option C - Avec Node.js :
```bash
npx serve .
```

---

## 🔧 Configuration

### config/config.js

```javascript
const CONFIG = {
    // Supabase
    SUPABASE_URL: 'https://xxx.supabase.co',
    SUPABASE_ANON_KEY: 'eyJhbGciOiJIUzI1NiIs...',
    
    // Google Sheets
    GOOGLE_SCRIPT_URL: 'https://script.google.com/macros/s/xxx/exec',
    GOOGLE_SHEET_ID: '1qKkOSPisPkqUQEkH-stKoUaEo1d9e63pVcV1iU9yvHw',
    
    // Digylog API
    DIGYLOG_API_URL: 'https://api.digylog.com/v2',
    DIGYLOG_TOKEN: '',
    
    // Store Info
    STORE_NAME: 'Hichoux Store',
    STORE_PHONE: '0600000000',
    WHATSAPP_NUMBER: '212600000000',
    
    // Shipping
    DEFAULT_SHIPPING_COST: 30,
    FREE_SHIPPING_THRESHOLD: 500,
    
    // Currency
    CURRENCY: 'DH',
    CURRENCY_CODE: 'MAD'
};
```

---

## 📖 Documentation

- [Guide d'Installation Complet](docs/INSTALLATION.md)
- [Documentation API](docs/API.md)
- [Guide de Déploiement](docs/DEPLOYMENT.md)

---

## 🔄 Workflow

```
Client passe commande → Statut: "new"
        ↓
Admin confirme (appel/WhatsApp) → Statut: "confirmed"
        ↓
Auto-sync vers Google Sheet
        ↓
Admin crée bordereau → API Digylog → Statut: "shipped"
        ↓
Tracking number généré
        ↓
Livraison → Statut: "delivered"
```

---

## 🛠️ Technologies

| Catégorie | Technologie |
|-----------|-------------|
| Frontend | HTML5, CSS3, JavaScript (Vanilla) |
| CSS | TailwindCSS (CDN) |
| Database | Supabase (PostgreSQL) |
| Auth | Supabase Auth |
| Storage | Supabase Storage |
| Realtime | Supabase Realtime |
| Sheets | Google Apps Script |
| Livraison | Digylog API |

---

## 📱 Responsive

Le site est optimisé pour :
- 📱 Mobile (320px+)
- 📱 Tablet (768px+)
- 💻 Desktop (1024px+)

---

## 🔐 Sécurité

- ✅ Row Level Security (RLS) sur toutes les tables
- ✅ Clés API séparées (anon vs service)
- ✅ Validation des données côté serveur
- ✅ Protection CORS

---

## 🤝 Contribution

Les contributions sont les bienvenues !

1. Fork le projet
2. Créer une branche (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Commit (`git commit -m 'Ajout nouvelle fonctionnalité'`)
4. Push (`git push origin feature/nouvelle-fonctionnalite`)
5. Ouvrir une Pull Request

---

## 📄 License

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 📞 Support

- 📧 Email: contact@hichouxstore.ma
- 💬 WhatsApp: +212 600 000 000

---

**Made with ❤️ in Morocco 🇲🇦**

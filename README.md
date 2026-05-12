# 🛡️ SecureShop — Cybersecurity Marketplace

> A full-featured e-commerce platform for cybersecurity products built on Orchard Core CMS with ASP.NET Core.

![SecureShop Banner](screenshots/home.png)

---

## 📌 Project Description

**SecureShop** is a cybersecurity-focused e-commerce marketplace where users can browse, compare, and purchase premium security software — VPNs, antivirus solutions, and password managers.

### Problem it solves
Finding trustworthy cybersecurity tools is difficult — users have to visit dozens of vendor websites, compare features manually, and have no unified checkout experience. SecureShop aggregates the best security products in one place with transparent pricing, ratings, and a secure checkout flow.

### Key highlights
- Users can browse products by category, search, and sort by price or rating
- Cryptographically secure password generator built to NIST SP 800-63B standards
- Full authentication system with registration, login, and user profiles
- Shopping cart persisted via localStorage with quantity management
- Mock payment flow with card form UI

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│                        Browser                          │
│         HTML / CSS / Vanilla JS / localStorage          │
└──────────────────────┬──────────────────────────────────┘
                       │ HTTP/HTTPS
┌──────────────────────▼──────────────────────────────────┐
│              Orchard Core 2.1 (ASP.NET Core 8)          │
│                                                         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │  Liquid     │  │  Razor Views │  │  Content      │  │
│  │  Templates  │  │  (Auth)      │  │  Management   │  │
│  └─────────────┘  └──────────────┘  └───────────────┘  │
│                                                         │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐  │
│  │  Users /    │  │  Media       │  │  AutoRoute    │  │
│  │  Auth       │  │  Library     │  │  Part         │  │
│  └─────────────┘  └──────────────┘  └───────────────┘  │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│           MS SQL Server (ShopDb)                        │
│   Content Items · Users · Media · Settings              │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| CMS | Orchard Core 2.1.0 |
| Backend | ASP.NET Core 8 / C# |
| Database | MS SQL Server |
| Templating | Liquid (Design → Templates) + Razor (.cshtml) |
| Frontend | Vanilla JS, CSS3 (no frameworks) |
| Fonts | Inter (Google Fonts) |
| Auth | OrchardCore.Users + OrchardCore.Users.Registration |
| Storage | localStorage (cart, avatar) |
| Crypto | `window.crypto.getRandomValues()` (CSPRNG) |

---

## 📦 Content Types

### Product
| Field | Type | Description |
|-------|------|-------------|
| TitlePart | — | Product name |
| AutoroutePart | — | URL slug |
| Price | Numeric | Current price |
| OldPrice | Numeric | Original price (for discount) |
| Period | Text | `/mo`, `/year`, `/lifetime` |
| Category | Text | VPN, Antivirus, Password Manager |
| Rating | Numeric | 0–5 stars |
| RatingCount | Numeric | Number of reviews |
| Description | TextArea | Product description |
| Features | TextArea | Feature list (one per line) |
| Image | Media | Product image |
| Badge | Text | BEST SELLER, TOP RATED, etc. |
| BadgeColor | Text | cyan, orange, green, purple |

---

## ⚙️ Setup & Run Instructions

### Prerequisites
- [.NET SDK 8.0+](https://dotnet.microsoft.com/download)
- MS SQL Server (local or remote)
- Git

### 1. Clone the repository
```bash
git clone https://github.com/rusalim45/InfoSecFinal
cd SecureShop/SecureShop.Web
```

### 2. Configure the database
Edit `appsettings.json`:
```json
{
  "ConnectionStrings": {
    "Default": "Server=YOUR_SERVER;Database=ShopDb;Trusted_Connection=True;TrustServerCertificate=True;"
  }
}
```

### 3. Run the project
```bash
dotnet run
```

### 4. Open in browser
```
https://localhost:5001
```

### 5. First-time setup
On first run, Orchard Core will prompt you to set up the site:
- Select **Blog** recipe
- Create admin account
- Database will be initialized automatically

### 6. Restore content
After setup, go to **Admin → Design → Templates** and restore the Liquid templates from the `/templates` folder in this repository.

---

## 🔐 Security Features

### Password Generator
- Uses `window.crypto.getRandomValues()` — CSPRNG (Cryptographically Secure Pseudo-Random Number Generator)
- Entropy calculation: **H = L × log₂(N)** where L = password length, N = charset size
- NIST SP 800-63B thresholds:
  - ⚠️ Weak: H < 40 bits
  - ⚡ Medium: 40 ≤ H < 60 bits
  - ✅ Strong: H ≥ 60 bits
- Crack time estimation at 1 trillion guesses/second

### Authentication
- Built on ASP.NET Core Identity via OrchardCore.Users
- Anti-forgery token protection on all POST requests
- Password hashing via ASP.NET Core Identity (PBKDF2)
- Remember Me with secure cookie

### Checkout
- Checkout button requires authentication
- Unauthenticated users are redirected to `/Login?ReturnUrl=/cart`
- Payment form is a UI mockup (no real payment processing)

---

## 📸 Screenshots

| Page | Preview |
|------|---------|
| Home | ![Home](screenshots/home.png) |
| Shop | ![Shop](screenshots/shop.png) |
| Product | ![Product](screenshots/product.png) |
| Cart | ![Cart](screenshots/cart.png) |
| Generator | ![Generator](screenshots/generator.png) |
| Login | ![Login](screenshots/login.png) |
| Profile | ![Profile](screenshots/profile.png) |

---

## 🎥 Demo Video

▶️ [Watch Demo](https://drive.google.com/file/d/1P3pmWtzhmPe89Fvn0e4LLMhrccXR10EM/view?usp=sharing)

---

## 👨‍🏫 Feedback

▶️ [Feedback Video](https://drive.google.com/file/d/1P3pmWtzhmPe89Fvn0e4LLMhrccXR10EM/view?usp=sharing)

*Feedback provided by , SFW Department, AUCA*

---

## 👤 Author

**Rustam Alimov**
American University of Central Asia
Information Security and Intro to Web Programing — Final Project, 2026

---

## 📄 License

This project is created for educational purposes as part of the Information Security course at AUCA.

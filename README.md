# Hi, I'm Nelson Macharia 👋🏾
**Full-Stack Developer (Junior) · Final-Year Computer Science Student · Kenya 🇰🇪**

I build practical full-stack systems for everyday people and small businesses in Kenya, with a focus on payments, delivery, and useful business workflows.

[![WhatsApp](https://img.shields.io/badge/WhatsApp-Chat%20with%20me-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/254719857793) [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nelson-macharia-97b715314/) [![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/macharianelson2024-art) [![Email](https://img.shields.io/badge/Email-macharianelson2024%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:macharianelson2024@gmail.com)

---

## 🧭 About Me

I'm a final-year student pursuing a Diploma in Computer Science in Kenya.

I'm a junior developer who learns by building, testing, listening to feedback, and improving the details that make software useful.

My main focus is full-stack development for real Kenyan problems, especially the needs of everyday users and small businesses.

I learn quickly, adapt to new tools, and enjoy working across the frontend, backend, data, and integrations of a product.

I'm open to junior developer roles, internships, freelance work, mentorship, and collaboration.

I'm early in my journey — but I build like it matters.

---

## 🛠️ What I Work With

**Frontend** — `JavaScript` · `HTML` · `ES modules` · `Tailwind CSS` · `Leaflet` · `React` · `TypeScript`

**Backend** — `Python` · `Django` · `Django REST Framework` · `JWT` · `Celery`

**Cloud & Realtime** — `Firebase Authentication` · `Firestore` · `Realtime Database` · `firebase-admin`

**Payments** — `Safaricom Daraja` · `M-Pesa STK Push` · `B2C payouts`

**Infrastructure** — `Docker` · `Nginx`

**Routing & Maps** — `OSRM` · `Esri World Street tiles`

---

## 🚀 Projects

### 01 · [Gmarketfy](https://github.com/macharianelson2024-art/gmarketfy-marketplace) — Multi-Vendor Marketplace for Kenya `Flagship`

Gmarketfy is a marketplace MVP that connects clients, vendors, and drivers through product discovery, ordering, M-Pesa payments, dispatch, live delivery tracking, and vendor payouts.

It is built around a clear boundary: **Django owns the money. Firebase owns product data. Daraja moves the cash.**

#### What it does

- **Clients** browse vendors, manage carts, place multi-item orders, pay through M-Pesa STK Push, and track deliveries with live GPS, road routes, and ETA.
- **Vendors** manage products, orders, drivers, plans, analytics, wallets, and withdrawals through M-Pesa B2C.
- **Drivers** receive deliveries, broadcast their location through Firebase Realtime Database, follow road routes, upload proof, and complete orders.

#### Engineering highlights

1. **Append-only wallet ledger** — Vendor balances are derived from ledger entries. Corrections use compensating entries, while a unique source constraint helps prevent double-crediting.

2. **Idempotent payment callbacks** — Daraja may retry callbacks, so handlers use row locking and terminal-status checks to make duplicate callbacks no-ops.

3. **Authoritative fee calculation** — The interface previews withdrawal fees locally, but Django recalculates the final charge during submission and remains the source of truth.

4. **One GPS stream, two views** — A single `watchPosition()` stream serves both the driver map and client tracking, with Realtime Database writes throttled by distance and time.

The repository contains the full architecture diagram, setup instructions, role details, payment flows, and implementation notes:

**[Explore Gmarketfy on GitHub →](https://github.com/macharianelson2024-art/gmarketfy-marketplace)**

#### Stack used in Gmarketfy

`Python` · `Django` · `Django REST Framework` · `JavaScript` · `HTML/ES modules` · `Tailwind CSS` · `Firebase` · `Daraja` · `Leaflet` · `OSRM` · `SQLite` · `Docker` · `Nginx`

### 02 · Coming soon

More builds landing soon — this list grows as I ship.

---

## 🧠 How I Think About Code

I prefer correctness over cleverness, especially when software handles money, identity, or delivery status.

I value auditability over convenience and try to keep important system behavior clear enough to inspect and explain.

I use real-time behavior where it adds value, and I choose simple, proven tools where simple is the right answer.

> Gmarketfy prioritizes correctness over cleverness, auditability over convenience, and real-time behavior where it matters.

---

## 📬 Let's Connect

Open to junior developer roles, internships, freelance work, mentorship, and collaboration.

[![WhatsApp](https://img.shields.io/badge/WhatsApp-Chat%20with%20me-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/254719857793) [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nelson-macharia-97b715314/) [![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/macharianelson2024-art) [![Email](https://img.shields.io/badge/Email-macharianelson2024%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:macharianelson2024@gmail.com)

**Built in Kenya, for Kenya. Open to feedback, collaboration, and hard problems.**

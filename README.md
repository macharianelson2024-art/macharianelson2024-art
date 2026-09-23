# Hi, I'm Nelson Macharia 👋🏾
**Full-Stack Developer (Junior) · Final-Year CS Student · Kenya 🇰🇪**

I build full-stack systems that make everyday work — payments, delivery, and small-business tools — easier for people in Kenya.

[![WhatsApp](https://img.shields.io/badge/WhatsApp-Chat%20with%20me-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/254719857793) [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nelson-macharia-97b715314/) [![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/macharianelson2024-art) [![Email](https://img.shields.io/badge/Email-macharianelson2024%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:macharianelson2024@gmail.com)

---

## 🧭 About Me

I'm Nelson, a final-year student pursuing a Diploma in Computer Science in Kenya.

I'm a junior developer who is already shipping real systems and learning through the details of building them.

I'm focused on full-stack products that solve everyday problems for Kenyan people and small businesses.

I learn quickly, adapt faster, and welcome feedback that helps me write clearer, more useful software.

I'm open to junior roles, internships, freelance work, mentorship, and collaboration.

I'm early in my journey — but I build like it matters.

---

## 🛠️ What I Work With

**Frontend** — `React` · `TypeScript` · `JavaScript` · `Tailwind CSS` · `HTML/ES modules` · `Leaflet`

**Backend** — `Python` · `Django` · `Django REST Framework` · `JWT` · `Celery`

**Cloud & Realtime** — `Firebase Auth` · `Firestore` · `Realtime Database` · `firebase-admin`

**Payments** — `Safaricom Daraja` (`M-Pesa STK Push` · `B2C payouts`)

**Infra & DevOps** — `Docker` · `Nginx`

**Routing & Maps** — `OSRM` · `Esri World Street tiles`

---

## 🚀 Projects

### 01 · Gmarketfy — Multi-Vendor Marketplace for Kenya  `Flagship`

> The complete commerce loop for the Kenyan market — vendors, clients, drivers, M-Pesa payments, and live delivery tracking in one system.

[View the Gmarketfy repository](https://github.com/macharianelson2024-art/gmarketfy-marketplace)

Gmarketfy is a multi-vendor marketplace platform that covers vendor onboarding, product listing, customer ordering, payment, dispatch, delivery tracking, and vendor payouts. Three frontend apps — `client/`, `vendor/`, and `driver/` — share Firebase for identity and product data, while **Django** remains the authoritative boundary for money.

**Django owns the money. Firebase owns product data. Daraja moves the cash.**

#### What it does

##### Clients

- Browse vendors and products, manage a cart, and place multi-item orders.
- Pay through M-Pesa STK Push with sending, PIN, polling, success, failure, and timeout states.
- Track drivers with live GPS, road routes, and ETA, then review order history, spend analytics, and saved addresses.

##### Vendors

- Manage products, orders, drivers, analytics, and store settings.
- Dispatch orders individually or in bulk and change between Free, Medium, Premium, and Ultimate plans through M-Pesa.
- Withdraw through M-Pesa B2C with plan-based fee handling and inspect a derived wallet balance, **append-only** `ledger`, and payout-destination audit trail.

##### Drivers

- Receive assigned deliveries, mark them in progress, and complete them with uploaded delivery proof.
- Broadcast live GPS through Firebase Realtime Database.
- Use a Google-Maps-style delivery view with heading, proximity-ranked stops, turn-by-turn banners, ETA, and real road routes.

#### Engineering highlights

1. **Append-only wallet ledger** — The vendor balance is derived by summing entries, never stored as a mutable value. Corrections are compensating entries, and a unique constraint on `(vendor_id, kind, source_type, source_id)` prevents double-crediting.

2. **Idempotent payment callbacks** — Daraja can retry callbacks. Handlers use `select_for_update()` and a terminal-status guard, so duplicate callbacks become no-ops instead of duplicate financial actions.

3. **Plan-based fee model** — Every withdrawal carries a flat 5% Gmarketfy fee. The plan controls the minimum withdrawal and who absorbs Safaricom's banded KSh 5–13 B2C fee. The full breakdown is stored on the `Withdrawal` row.

4. **One GPS stream, two views** — A single `watchPosition()` call feeds the driver and client views through a callback registry. Realtime Database writes are throttled at 10 m of movement or 5 s of elapsed time.

5. **Preview locally, charge authoritatively** — The withdrawal modal previews fees on every keystroke without API calls. The backend recalculates the charge at submission and remains the source of truth.

6. **Google-Maps-style route rendering** — Three stacked polylines — shadow, casing, and core — improve route visibility. Stops are proximity-ranked, with the casing paired to the turn banner and maneuver display.

#### Architecture

```text
 client/                         vendor/                         driver/
    |                               |                               |
    | Authorization: Bearer <id_token>                              |
    +-------------------------------+-------------------------------+
                                    |
                                    v
                         +---------------------------+
                         | Django API                |
                         | vendors_and_transactions  |
                         | vendors_plans             |
                         | vendor_wallet             |
                         | utilities                 |
                         +------------+--------------+
                                      |
                   +------------------+------------------+
                   |                                     |
                   v                                     v
        +-------------------------+           +-------------------------+
        | Firebase                |           | Daraja / M-Pesa         |
        | Authentication         |           | STK Push: incoming      |
        | Firestore               |           | B2C: vendor payouts     |
        | Realtime Database       |           | callbacks -> Django     |
        +-------------------------+           +------------+------------+
          | identity, vendors,                              |
          | products, orders, drivers,                      |
          | delivery proofs, live GPS                       |
          |                                                  |
          +<----- one-way payment-state sync ---------------+
                 Django -> Firestore
                 never the reverse
```

The three frontends send Firebase ID tokens to the Django API through `Authorization: Bearer <id_token>`. Firebase handles authentication, product and operational data, delivery proofs, and live GPS updates.

Django verifies identity, owns financial records, and receives Daraja callbacks for STK Push and B2C activity. Payment state moves in a **one-way sync** from Django to Firestore, never back toward Django.

> ### 🔐 The money boundary
> Django is the only service allowed to mutate financial state. Firebase is read-mostly for money. The sync is one-way — Django to Firestore — never the reverse.

#### Stack for this project

`Django` · `DRF` · `React` · `TypeScript` · `Tailwind` · `Firebase Auth` · `Firestore` · `Realtime DB` · `Daraja` · `Celery` · `Docker` · `Nginx`

#### Getting started

##### Backend

```bash
cd backend/Gmarketfy
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
# Configure Daraja environment variables and a secure Firebase Admin JSON path
python manage.py migrate && python manage.py seed_plans
python manage.py runserver
```

##### Frontend

```bash
# No frontend build step is required
python -m http.server 5500
# Open the relevant entry point under client/, vendor/, or driver/
```

##### M-Pesa callbacks via ngrok

```bash
ngrok http 8000
# Use the HTTPS forwarding URL for Daraja callback configuration
```

> Callback endpoints stay on Django and must never reach the frontend. Never commit credentials, tokens, API keys, or Firebase service-account contents.

#### Roadmap

- WebSocket updates for withdrawal status
- Administrative reporting dashboard
- Self-hosted OSRM
- Operational notifications
- Scheduled vendor payouts
- Multi-currency support

### 02 · (Coming soon)

More builds landing soon — this list grows as I ship.

---

## 🧠 How I Think About Code

I choose correctness over cleverness, especially when money, identity, and delivery status are involved.

I prefer auditability over convenience, with clear records and boundaries that make behavior easier to inspect.

I use real-time behavior where it matters and boring tools where boring is right.

> Gmarketfy prioritizes correctness over cleverness, auditability over convenience, and real-time behavior where it matters.

---

## 📬 Let's Connect

Open to junior developer roles, internships, freelance work, mentorship, and collaboration.

[![WhatsApp](https://img.shields.io/badge/WhatsApp-Chat%20with%20me-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/254719857793) [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nelson-macharia-97b715314/) [![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/macharianelson2024-art) [![Email](https://img.shields.io/badge/Email-macharianelson2024%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:macharianelson2024@gmail.com)

**Built in Kenya, for Kenya. Open to feedback, collaboration, and hard problems.**

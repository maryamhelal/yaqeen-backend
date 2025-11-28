# Yaqeen Backend

Lightweight Node.js / Express backend for the Yaqeen API (e-commerce features: users, products, orders, promo codes, messages, etc.).

**Quick overview:**

- **Language:** JavaScript (Node.js + Express)
- **Database:** MongoDB (via Mongoose)
- **Email:** Nodemailer (Gmail service in current config)
- **API docs:** Swagger (see `swagger.js` and `README-Swagger.md`)

**Installation**

1. Clone the repository:

```bash
git clone https://github.com/maryamhelal/yaqeen-backend.git
cd yaqeen-backend
```

2. Install dependencies:

```bash
npm install
```

**Environment variables**

Create a `.env` file in the project root (or set environment variables in your host). The app expects the following variables:

- `PORT` — (optional) port to run the server (default: `5000`)
- `MONGO_URI` — MongoDB connection string
- `JWT_SECRET` — secret used to sign JSON Web Tokens
- `EMAIL_USER` — email address used to send emails (configured for Gmail service)
- `EMAIL_PASS` — password or app password for the `EMAIL_USER`

Example `.env`:

```
PORT=5000
MONGO_URI=mongodb://localhost:27017/yaqeen
JWT_SECRET=your_jwt_secret_here
EMAIL_USER=your@gmail.com
EMAIL_PASS=yourEmailPasswordOrAppPassword
```

Security note: When using Gmail you may need to create an App Password or allow less secure apps depending on your account settings. Prefer app passwords with 2FA enabled.

**Run the app**

- Development (auto-reload):

```bash
npm run dev
```

- Production:

```bash
npm start
```

The server entrypoint is `server.js`.

**API documentation (Swagger)**

- Swagger is provided via `swagger.js`. See `README-Swagger.md` and `swagger-tests.md` for details on available endpoints and examples.

**Project structure (important files/folders)**

- `server.js` — application bootstrap
- `routes/` — Express routes (admins, auth, cities, messages, orders, products, promocodes, sales, tags, unsubscribe, users)
- `controllers/` — route handlers and business logic
- `models/` — Mongoose models
- `services/` — reusable services (email, orders, products, messages, etc.)
- `middleware/` — Express middleware (authentication, uploads)
- `repos/` — repository-style data access (where present)
- `utils/` — helper utilities and email templates
- `uploads/` — uploaded files (images)

**Important routes (overview)**

The repo provides typical e-commerce-related endpoints grouped by route file. Browse the `routes/` folder to discover:

- Authentication (`routes/auth.js`) — login, register, OTP flows
- Users (`routes/users.js`) — user management
- Products (`routes/products.js`) — product CRUD and uploads
- Orders (`routes/orders.js`) — order creation and management
- Messages, promos, tags, cities, unsubscribe — see respective route files

**Scripts**

- `npm run dev` — start server with `nodemon` for development
- `npm start` — run `node server.js` (production)

**Docker**

There is a `Dockerfile` in the repo root. You can build and run the image with Docker if you prefer containerized runs.

Example build & run:

```powershell
docker build -t yaqeen-backend .
docker run -e MONGO_URI="your_mongo_uri" -e JWT_SECRET="secret" -e EMAIL_USER="you" -e EMAIL_PASS="pass" -p 5000:5000 yaqeen-backend
```

**Troubleshooting**

- If `npm run dev` exits with an error, check the console for stack traces and verify your `.env` values, especially `MONGO_URI` and `JWT_SECRET`.
- Email sending uses Gmail via `nodemailer` — ensure `EMAIL_USER`/`EMAIL_PASS` are correct and that the account allows SMTP access (app password recommended).

**Testing & API exploration**

- Use the Swagger UI (see `swagger.js`) or import `swagger-tests.md` / `README-Swagger.md` to try the routes.
- You can also use Postman or HTTP clients to exercise the routes present in `routes/`.

**Contributing**

- Open an issue or pull request. Keep changes focused and add tests where appropriate.

# SmartFlow Traffic UI — Complete Setup & Render Deployment Guide

---

## 📁 Final Project Structure

```
smartflow-traffic-ui/
├── src/
│   └── main/
│       ├── java/com/smartflow/
│       │   ├── SmartFlowApplication.java
│       │   ├── controller/
│       │   │   ├── PageController.java
│       │   │   └── TrafficController.java
│       │   ├── model/
│       │   │   └── TrafficData.java
│       │   ├── repository/
│       │   │   └── TrafficRepository.java
│       │   └── service/
│       │       └── TrafficService.java
│       └── resources/
│           ├── application.properties
│           └── templates/
│               └── index.html
├── Dockerfile
├── pom.xml
└── .gitignore
```

---

## 🖥️ Step 1 — Run Locally (VS Code)

### Prerequisites
- Java 17 installed → `java -version`
- Maven installed → `mvn -version`
- VS Code with **Extension Pack for Java** installed

### Steps
1. Open the project folder in VS Code: `File → Open Folder`
2. Open terminal in VS Code (`Ctrl + ~`)
3. Run: `mvn spring-boot:run`
4. Open browser → `http://localhost:10000`
5. H2 console (dev only) → `http://localhost:10000/h2-console`
   - JDBC URL: `jdbc:h2:mem:trafficdb`
   - User: `sa`, Password: *(blank)*

---

## ☁️ Step 2 — Push to GitHub

```bash
# 1. Initialise git (if not done)
git init
git add .
git commit -m "SmartFlow Traffic UI - initial commit"

# 2. Create a new repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/smartflow-traffic-ui.git
git branch -M main
git push -u origin main
```

---

## 🚀 Step 3 — Deploy on Render (Free Tier)

### Option A — Docker Deploy (Recommended)

1. Go to **https://render.com** → Sign in / Sign up (free)
2. Click **"New +"** → **"Web Service"**
3. Connect your **GitHub** account and select your `smartflow-traffic-ui` repo
4. Fill in the settings:

| Field | Value |
|-------|-------|
| Name | `smartflow-traffic-ui` |
| Region | Singapore (closest to Pune) |
| Branch | `main` |
| Runtime | **Docker** |
| Instance Type | **Free** |

5. Click **"Create Web Service"**

Render will automatically detect the `Dockerfile`, build the image, and deploy.

### Option B — Direct JAR Deploy

If you don't want Docker:

| Field | Value |
|-------|-------|
| Runtime | **Java** |
| Build Command | `mvn clean package -DskipTests` |
| Start Command | `java -jar target/traffic-ui-1.0.jar` |

---

## 🔧 Step 4 — Environment Variables on Render

By default the app uses **H2 in-memory** DB (no setup needed).

If you want **MySQL** (Render offers a free MySQL add-on):

Go to your web service → **Environment** tab → Add:

| Key | Value |
|-----|-------|
| `DB_URL` | `jdbc:mysql://your-mysql-host:3306/trafficdb` |
| `DB_USER` | `root` |
| `DB_PASS` | `yourpassword` |
| `DB_DRIVER` | `com.mysql.cj.jdbc.Driver` |
| `DB_PLATFORM` | `org.hibernate.dialect.MySQLDialect` |
| `PORT` | `10000` |

---

## ✅ Step 5 — Access Your Live App

After deployment (takes ~3–5 min), Render gives you a URL like:
```
https://smartflow-traffic-ui.onrender.com
```

> **Note:** Free tier spins down after 15 min of inactivity. First request after sleep takes ~30 sec to wake up.

---

## 🔄 Auto-Deploy on Code Changes

Every time you push to GitHub `main` branch, Render automatically redeploys. No manual steps needed.

```bash
# Make changes, then:
git add .
git commit -m "Updated UI"
git push
# → Render auto-redeploys in ~2 min
```

---

## 🐛 Troubleshooting

| Problem | Fix |
|---------|-----|
| App not starting | Check Render logs → "Logs" tab |
| Port error | Make sure `server.port=${PORT:10000}` is in application.properties |
| DB error | Switch to H2 by removing DB_* env vars |
| White label error | Make sure `index.html` is in `src/main/resources/templates/` |
| Build fails | Run `mvn clean package -DskipTests` locally first to verify |

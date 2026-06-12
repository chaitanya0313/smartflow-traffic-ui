# SmartFlow — Advanced Traffic Management System

A full-stack web application for real-time traffic monitoring and management, 
built with Spring Boot and deployed on Render.

## 🚦 Live Demo
🔗 [https://smartflow-traffic-ui.onrender.com](https://smartflow-traffic-ui.onrender.com)
> Note: Free tier on Render sleeps after 15 min of inactivity. 
> First load may take ~30 seconds to wake up.

## Features

- **Vehicle Entry Form** — Input Vehicle ID, Speed, Zone, and Status
- **Traffic Signal Indicator** — Visual signal (Red/Yellow/Green) based on traffic status
- **Emergency Vehicle Processing** — Special flag for emergency vehicle handling
- **Live Traffic Table** — Displays ID, Zone, Speed, Status, Process type, and Timestamp
- **Speed Chart** — Bar chart showing real-time speed data per zone
- **Action Buttons** — Process, Add, Refresh, and Clear controls

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 17, Spring Boot |
| Frontend | HTML, CSS, JavaScript |
| Database | H2 (In-Memory) |
| Build Tool | Maven |
| Deployment | Render (Docker) |

## Project Structure

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

## How to Run Locally

### Prerequisites
- Java 17
- Maven

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/chaitanya0313/smartflow-traffic-ui.git
cd smartflow-traffic-ui
```

**2. Run the application**
```bash
mvn spring-boot:run
```

**3. Open in browser**
http://localhost:10000

**4. H2 Database Console (optional)**
http://localhost:10000/h2-console

JDBC URL : jdbc:h2:mem:trafficdb

User    : sa

Password : (leave blank)

## Author

**Chaitanya Pingle**  
[GitHub](https://github.com/chaitanya0313)

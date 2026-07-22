[statistiques.html](https://github.com/user-attachments/files/30278110/statistiques.html)
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Statistiques</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Arial, Helvetica, sans-serif;
    }

    body {
      background: #0f172a;
      color: white;
      min-height: 100vh;
    }

    /* ================= HEADER (RESPONSIVE) ================= */
    header {
      height: 75px;
      background: linear-gradient(90deg, #102542, #163b69);
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 20px;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.35);
    }

    .logo {
      color: white;
      font-size: 1.3rem;
      font-weight: bold;
    }

    nav {
      display: flex;
      align-items: center;
      gap: 15px;
      width: 100%;
    }

    nav a {
      text-decoration: none;
      color: #d8e8ff;
      font-weight: bold;
      position: relative;
      transition: 0.25s;
      padding: 8px 12px;
      border-radius: 5px;
    }

    nav a:hover {
      color: #5eb5ff;
      background: rgba(94, 181, 255, 0.1);
    }

    nav a::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: 0;
      width: 0;
      height: 2px;
      background: #5eb5ff;
      transition: 0.25s;
    }

    nav a:hover::after {
      width: 100%;
    }

    nav a.active {
      color: #5eb5ff;
      background: rgba(94, 181, 255, 0.2);
    }

    nav a.active::after {
      width: 100%;
    }

    /* ================= SWITCH ================= */
    .switch {
      position: relative;
      width: 180px;
      height: 40px;
      background: #243b5e;
      border-radius: 50px;
      cursor: pointer;
      overflow: hidden;
      display: flex;
      align-items: center;
      padding: 4px;
      user-select: none;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
    }

    .switch .bubble {
      position: absolute;
      width: 85px;
      height: 32px;
      background: #3b82f6;
      border-radius: 50px;
      left: 4px;
      transition: 0.35s ease;
    }

    .switch.active .bubble {
      left: 87px;
    }

    .switch .label {
      position: relative;
      width: 50%;
      text-align: center;
      z-index: 2;
      color: white;
      font-weight: bold;
      font-size: 12px;
      transition: 0.3s;
    }

    .switch.active .left {
      color: #bdd3ff;
    }

    .switch:not(.active) .right {
      color: #bdd3ff;
    }

    /* ================= MAIN ================= */
    main {
      padding: 20px;
    }

    @media (min-width: 768px) {
      main {
        padding: 40px;
      }
    }

    h2 {
      color: #d8e8ff;
      margin-bottom: 10px;
    }

    .subtitle {
      color: #94a3b8;
      font-size: 14px;
      margin-bottom: 30px;
    }

    /* ================= STATS CARDS ================= */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      margin-bottom: 30px;
    }

    @media (min-width: 768px) {
      .stats-grid {
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
        margin-bottom: 40px;
      }
    }

    .seance-card {
      background: #1e293b;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
      transition: transform 0.25s, box-shadow 0.25s;
    }

    .seance-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    }

    .seance-card .value {
      font-size: 28px;
      font-weight: 700;
      color: #5eb5ff;
      margin-bottom: 10px;
    }

    @media (min-width: 768px) {
      .seance-card .value {
        font-size: 36px;
      }
    }

    .seance-card .label {
      color: #94a3b8;
      font-size: 13px;
    }

    /* ================= GRAPHIQUE ================= */
    .chart-container {
      background: #1e293b;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
      margin-top: 20px;
      position: relative;
      height: 300px;
    }

    @media (min-width: 768px) {
      .chart-container {
        padding: 30px;
        height: 400px;
      }
    }

    .chart-container h3 {
      color: #d8e8ff;
      margin-bottom: 20px;
      text-align: center;
    }

    /* ================= FOOTER ================= */
    footer {
      background: #102542;
      text-align: center;
      padding: 15px;
      color: #94a3b8;
      font-size: 12px;
    }

    @media (min-width: 768px) {
      footer {
        padding: 20px;
        font-size: 14px;
      }
    }
  </style>
</head>

<body>
  <header>
    <div class="logo">
      vocva
    </div>

    <nav>
      <a href="index.html">Séances</a>
      <a href="historique.html">Historique</a>
      <a href="statistiques.html" class="active">Statistiques</a>
    </nav>

    <div class="switch" id="switch">
      <div class="bubble"></div>
      <div class="label left">Apprenant</div>
      <div class="label right">Éditeur</div>
    </div>
  </header>

  <main>
    <div>
      <h2>Statistiques</h2>
      <p class="subtitle">Votre progression globale.</p>
    </div>

    <div class="stats-grid">
      <div class="seance-card">
        <div class="value" id="statsSeances">0</div>
        <div class="label">Séances créées</div>
      </div>

      <div class="seance-card">
        <div class="value" id="statsMots">0</div>
        <div class="label">Mots au total</div>
      </div>

      <div class="seance-card">
        <div class="value" id="statsTentatives">0</div>
        <div class="label">Tentatives saisies</div>
      </div>

      <div class="seance-card">
        <div class="value" id="statsTaux">0%</div>
        <div class="label">Taux de réussite</div>
      </div>
    </div>

    <div class="chart-container">
      <h3>Évolution du taux de réussite</h3>
      <canvas id="successRateChart"></canvas>
    </div>
  </main>

  <footer>© 2026 Plateforme éducative</footer>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/12.16.0/firebase-app.js";
    import {
      getFirestore,
      collection,
      getDocs
    } from "https://www.gstatic.com/firebasejs/12.16.0/firebase-firestore.js";

    const firebaseConfig = {
      apiKey: "AIzaSyDs71URHtBAQ93FlFXhCGBws4bwcUxecBY",
      authDomain: "orthographe-ab78d.firebaseapp.com",
      projectId: "orthographe-ab78d",
      storageBucket: "orthographe-ab78d.firebasestorage.app",
      messagingSenderId: "819962816708",
      appId: "1:819962816708:web:e9017361478dc68faa0191",
      measurementId: "G-70L5EVEWPJ"
    };

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Variables globales
    let sessionsData = [];
    let mode = "Apprenant";
    let successRateChart = null;

    // Récupérer les séances depuis Firestore
    async function fetchSessions() {
      try {
        const seancesRef = collection(db, "sessions");
        const querySnapshot = await getDocs(seancesRef);
        sessionsData = [];
        querySnapshot.forEach((doc) => {
          const session = doc.data();
          sessionsData.push({
            id: doc.id,
            ...session
          });
        });
        chargerStats();
      } catch (error) {
        console.error("Erreur:", error);
      }
    }

    // Charger les statistiques et créer le graphique
    async function chargerStats() {
      try {
        let totalMots = 0;
        let tentativesRemplies = 0;
        let reussites = 0;
        const sessionDataForChart = [];

        sessionsData.forEach((session) => {
          const mots = Array.isArray(session.mots) ? session.mots : [];
          const attempts = Array.isArray(session.userAttempts) ? session.userAttempts : [];
          const createdAt = session.createdAt ? new Date(session.createdAt) : null;
          const score = session.score || 0;
          const total = session.total || mots.length;

          totalMots += mots.length;

          let sessionReussites = 0;
          attempts.forEach((attempt, idx) => {
            if (attempt && attempt.toString().trim() !== "") {
              tentativesRemplies++;
            }
            if (mots[idx] && attempt && attempt.toString().trim().toLowerCase() === mots[idx].toString().trim().toLowerCase()) {
              sessionReussites++;
              reussites++;
            }
          });

          if (createdAt && total > 0) {
            const dateStr = createdAt.toLocaleDateString("fr-FR");
            const successRate = Math.round((sessionReussites / total) * 100);
            sessionDataForChart.push({
              date: dateStr,
              successRate: successRate,
              total: total
            });
          }
        });

        const tauxReussite = totalMots > 0 ? Math.round((reussites / totalMots) * 100) : 0;

        document.getElementById("statsSeances").textContent = sessionsData.length;
        document.getElementById("statsMots").textContent = totalMots;
        document.getElementById("statsTentatives").textContent = tentativesRemplies;
        document.getElementById("statsTaux").textContent = tauxReussite + "%";

        createSuccessRateChart(sessionDataForChart);

      } catch (error) {
        console.error("Erreur:", error);
      }
    }

    // Créer le graphique avec Chart.js
    function createSuccessRateChart(sessionData) {
      if (sessionData.length === 0) {
        console.warn("Aucune donnée disponible pour le graphique.");
        return;
      }

      sessionData.sort((a, b) => new Date(a.date) - new Date(b.date));

      const dates = sessionData.map(item => item.date);
      const successRates = sessionData.map(item => item.successRate);

      const ctx = document.getElementById('successRateChart').getContext('2d');

      if (successRateChart) {
        successRateChart.destroy();
      }

      successRateChart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: dates,
          datasets: [{
            label: 'Taux de réussite (%)',
            data: successRates,
            borderColor: '#5eb5ff',
            backgroundColor: 'rgba(94, 181, 255, 0.1)',
            borderWidth: 2,
            tension: 0.4,
            fill: true,
            pointBackgroundColor: '#5eb5ff',
            pointBorderColor: '#fff',
            pointBorderWidth: 1,
            pointRadius: 5,
            pointHoverRadius: 7
          }]
        },
        options: {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            y: {
              beginAtZero: true,
              max: 100,
              ticks: {
                color: '#94a3b8',
                callback: function(value) {
                  return value + '%';
                }
              },
              grid: {
                color: 'rgba(255, 255, 255, 0.1)'
              }
            },
            x: {
              ticks: {
                color: '#94a3b8',
                maxRotation: 45,
                minRotation: 45
              },
              grid: {
                color: 'rgba(255, 255, 255, 0.1)'
              }
            }
          },
          plugins: {
            legend: {
              labels: {
                color: '#d8e8ff'
              }
            },
            tooltip: {
              callbacks: {
                label: function(context) {
                  return context.dataset.label + ': ' + context.parsed.y + '%';
                }
              }
            }
          }
        }
      });
    }

    // Gestion du switch
    const sw = document.getElementById("switch");
    sw.addEventListener("click", () => {
      sw.classList.toggle("active");
      mode = sw.classList.contains("active") ? "Éditeur" : "Apprenant";
    });

    // Charger les séances au démarrage
    document.addEventListener('DOMContentLoaded', () => {
      fetchSessions();
    });
  </script>
</body>
</html>

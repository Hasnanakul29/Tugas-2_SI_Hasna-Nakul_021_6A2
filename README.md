<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>3-Day Weather Forecast - Klojen</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f4f8;
      padding: 20px;
    }
    .container {
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      max-width: 800px;
      margin: auto;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
    }
    th {
      background-color: #007bff;
      color: white;
    }
    footer {
      text-align: center;
      margin-top: 20px;
      font-size: 0.9em;
      color: #777;
    }
  </style>
</head>
<body>

<div class="container">
  <h2>3-Day Weather Forecast - Kecamatan Klojen</h2>
  <table id="weather-table">
    <thead>
      <tr>
        <th>Date</th>
        <th>Max Temp (°C)</th>
        <th>Min Temp (°C)</th>
        <th>Precipitation (mm)</th>
      </tr>
    </thead>
    <tbody>
      <!-- Data will be inserted here -->
    </tbody>
  </table>

  <footer>
    Dibuat oleh Hasna Nakul_021_6A2 - Integrasi API OpenMeteo 2025
  </footer>
</div>

<script>
const API_URL = "https://api.open-meteo.com/v1/forecast?latitude=-7.973&longitude=112.6087&daily=temperature_2m_max,temperature_2m_min,precipitation_sum&timezone=Asia%2FBangkok&forecast_days=3";

fetch(API_URL)
  .then(response => response.json())
  .then(data => {
    const dates = data.daily.time;
    const maxTemps = data.daily.temperature_2m_max;
    const minTemps = data.daily.temperature_2m_min;
    const precipitation = data.daily.precipitation_sum;

    const tableBody = document.querySelector("#weather-table tbody");
    for (let i = 0; i < dates.length; i++) {
      const row = `
        <tr>
          <td>${dates[i]}</td>
          <td>${maxTemps[i]}</td>
          <td>${minTemps[i]}</td>
          <td>${precipitation[i]}</td>
        </tr>
      `;
      tableBody.innerHTML += row;
    }
  })
  .catch(error => {
    console.error("Error fetching data:", error);
    alert("Gagal mengambil data cuaca. Silakan cek koneksi internet atau URL API.");
  });
</script>

</body>
</html>

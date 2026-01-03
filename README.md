<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Исторические деревни Минска</title>
  
  <!-- Leaflet CSS -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <style>
    body { margin: 0; padding: 0; font-family: Arial, sans-serif; }
    #map { height: 100vh; width: 100%; }
    .info-box {
      position: absolute;
      top: 10px;
      right: 10px;
      width: 300px;
      max-height: 90vh;
      overflow-y: auto;
      background: white;
      padding: 15px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.3);
      z-index: 1000;
      display: none;
    }
    .info-box h2 { margin-top: 0; color: #2c3e50; }
    .close-btn {
      float: right;
      cursor: pointer;
      font-weight: bold;
      font-size: 18px;
    }
  </style>
</head>
<body>

<div id="map"></div>
<div class="info-box" id="infoBox">
  <span class="close-btn" onclick="closeInfo()">×</span>
  <div id="infoContent"></div>
</div>

<!-- Leaflet JS -->
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<script>
  // Центрируем карту на Минске
  const map = L.map('map').setView([53.8930, 27.4910], 13);

  // Подложка OpenStreetMap
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  // Данные деревень
  const villages = [
    {
      name: "Альшево",
      coords: [53.8975, 27.4750],
      text: "Альшево (в цифровых источниках Ольшево) — одна из старейших деревень-фольварков на северо-западе Минска, в 400 м севернее Кальварийского кладбища. В XVIII–XIX вв. принадлежало дворянам (Менделеевым, Шункевичам, Рихтерам). В 1959 г. включено в черту Минска, застройка снесена в 1960–70-х. Сегодня — район улиц Притыцкого, Ольшевского, Харьковской и Тимирязева. От фольварка ничего не осталось, но топоним жив."
    },
    {
      name: "Тиволи",
      coords: [53.8820, 27.4850],
      text: "Тиволи — романтичное дачное имение XIX века. Название дано в честь парка Tivoli в Копенгагене. Владелица Пелагея Монюшко (родственница композитора) разбила парк; позже Гольцберги открыли летний театр и ресторан. Здесь бывал Станислав Монюшко. В 1978 г. включено в город, в 1980–90-х снесено. Сегодня — ТРЦ «Тивали», парк, пруд и кинотеатр «Аврора»."
    },
    {
      name: "Медвежино",
      coords: [53.8770, 27.4650],
      text: "Медвежино упоминается с 1582 г. Название — от медведей или прозвища владельца. В XIX в. — 23 двора, 150 жителей. На Брестском тракте стояла знаменитая корчма с пивом и вывеской-медведем. Снесена в 1936 г. В 1962 г. включено в Минск, застройка утрачена. Сегодня — микрорайоны, школа №225, метро «Малиновка»."
    },
    {
      name: "Барановщина",
      coords: [53.8890, 27.4600],
      text: "Барановщина — деревня западнее Тиволи, рядом с нынешним рынком «Западный» и метро «Кунцевщина». В XIX в. — имение Гольцбергов (каменный дом, аптека в Минске). В 1978 г. включена в город, в 1980–90-х полностью снесена. Название, вероятно, от фамилии Баран(ов)."
    },
    {
      name: "Погулянка",
      coords: [53.8850, 27.4950],
      text: "Погулянка (фольварк «Широкое Болото») — от «гуляющих» (паровых) полей. До 1848 г. — Арамовичи, затем продана Сомковичам. В 1879–85 гг. арендатор нанёс ущерб и был выселен. В 1978 г. включена в Минск, в 1980-х застроена. Сегодня — ОАО «Сукно» и жилые кварталы у ул. Матусевича."
    }
  ];

  // Добавляем маркеры
  villages.forEach(v => {
    const marker = L.marker(v.coords).addTo(map);
    marker.on('click', () => {
      document.getElementById('infoContent').innerHTML = 
        `<h2>${v.name}</h2><p>${v.text}</p>`;
      document.getElementById('infoBox').style.display = 'block';
    });
  });

  function closeInfo() {
    document.getElementById('infoBox').style.display = 'none';
  }
</script>
</body>
</html>

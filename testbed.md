---
layout: page
title: Anycast Testbed
---

TANGLED was conceived in 2016, during a BGP hackathon organized by CAIDA/UCSD. The first release of the TANGLED was presented during <a href="https://ripe73.ripe.net/archives/video/1429/">RIPE73 </a> meeting.
In the following years, we expanded the testbed, deploying anycast sites around the world.

The anycast research testbed has been created within the context of <a
href="https://www.utwente.nl/en/eemcs/dacs/">DACS</a>, a consortium
consisting of the University of Twente, SIDN Labs, NLnet Labs and
SURFnet.

<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic" />
<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,600italic,700italic,800italic,400,300,600,700,800" />

Address prefixes and ASN resources have been allocated by SURFnet and
RIPE NCC.

IPv4: 145.100.118.0/23<br>
IPv4: 145.116.218.0/23<br>
IPv6: 2001:610:9000::/40  <br>
<a href="https://apps.db.ripe.net/db-web-ui/#/lookup?source=RIPE&type=route&key=145.100.118.0%2F23AS1149">ASN 1149</a>
<hr>

The testbed currently in expansion and already has several locations
either operational or being installed.

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<div id="testbed-map" style="width:100%;height:480px;margin-bottom:1em;"></div>

<style>
.badge-vultr    { background-color:#007bff;color:white;padding:2px 8px;border-radius:4px;font-size:.85em; }
.badge-melbicom { background-color:#e67e22;color:white;padding:2px 8px;border-radius:4px;font-size:.85em; }
.badge-both     { background-color:#6f42c1;color:white;padding:2px 8px;border-radius:4px;font-size:.85em; }
.vp-table { border-collapse:collapse;width:100%;font-size:.92em; }
.vp-table th { border-bottom:2px solid #ddd;padding:6px 10px;cursor:pointer;user-select:none;white-space:nowrap; }
.vp-table th:hover { background:#f5f5f5; }
.vp-table td { padding:4px 10px;border-bottom:1px solid #f0f0f0; }
.vp-table tbody tr:hover td { background:#f5f5f5;cursor:pointer; }
.vp-table tbody tr.vp-selected td { background:#fff3cd; }
.sort-arrow { font-size:.75em;margin-left:3px;opacity:.5; }
</style>

<p style="margin-top:.5em;">
  <span class="badge-vultr">Vultr</span>&nbsp;
  <span class="badge-melbicom">Melbicom</span>&nbsp;
  <span class="badge-both">Vultr + Melbicom</span>
  &nbsp;—&nbsp; Click a column header to sort. Click a row to highlight it on the map.
</p>

<table class="vp-table" id="vp-table">
<thead><tr>
  <th onclick="vpSort(0)">Location<span class="sort-arrow" id="vp-arr-0"></span></th>
  <th onclick="vpSort(1)">City<span class="sort-arrow" id="vp-arr-1"></span></th>
  <th onclick="vpSort(2)">Country<span class="sort-arrow" id="vp-arr-2"></span></th>
  <th onclick="vpSort(3)">Continent<span class="sort-arrow" id="vp-arr-3"></span></th>
  <th onclick="vpSort(6)">Provider<span class="sort-arrow" id="vp-arr-6"></span></th>
</tr></thead>
<tbody id="vp-tbody"></tbody>
</table>

<p style="margin-top:1.2em;">
  The <a href="https://manycast.net">LACeS census</a> (manycast.net) is performed using Vultr only.
</p>

<br>
<hr>

<div class="col-sm-10 col-sm-offset-0">
    <div class="row text-center" style="align:left;text-align: left;margin-top: 10px;">
        Some other institutions are supporting our deployments:
        <ul>
         <li><a href="https://www.ripe.net/" target="_blank">RIPE NCC</a></li>
         <li><a href="http://www.fiu.edu/" target="_blank">Florida International University</a></li>
         <li><a href="http://www.isi.edu/home" target="_blank">USC/Information Sciences Institute</a></li>
         <li><a href="https://www.dk-hostmaster.dk/english" target="_blank">DK Hostmaster</a></li>
         <li><a href="https://www.sidnlabs.nl" target="_blank">SIDN Labs</a></li>
     </ul>
     <br>
     We are also thankful to Nat Morris and John Heidemann for their support.
 </div>
</div>

<div class="container-fluid" style="margin: 0% 25% 0% 25%">
<div class="col-sm-12 col-sm-offset-0">
    <div class="row text-center"><br>
            <a href="http://www.utwente.nl/"><img src="/img/twente.png"></a>
            <a href="http://www.sidn.nl/"><img src="/img/sidn-logo.png"></a>
            <a href="https://nlnetlabs.nl/"><img src="/img/nlnetlab.png"></a>
            <a href="https://surfnet.nl/"><img src="/img/surfnet.png"></a>
            <a href="https://nwo.nl/"><img src="/img/nwo.jpg"></a>
    </div>
</div>
</div>

<script>
// [location, city, country, continent, lat, lon, provider]
var vpSites = [
  ["br-sao", "São Paulo",    "Brazil",        "South America", -23.5471, -46.6372, "Vultr"],
  ["us-hnl", "Honolulu",     "USA",           "North America",  21.3078,-157.8592, "Vultr"],
  ["nl-ams", "Amsterdam",    "Netherlands",   "Europe",         52.3785,   4.8998, "Vultr"],
  ["us-atl", "Atlanta",      "USA",           "North America",  33.7884, -84.4433, "Vultr"],
  ["in-blr", "Bangalore",    "India",         "Asia",           12.9762,  77.6033, "Vultr"],
  ["us-ord", "Chicago",      "USA",           "North America",  42.0067, -88.0048, "Vultr"],
  ["us-dfw", "Dallas",       "USA",           "North America",  32.7870, -96.7983, "Vultr"],
  ["in-del", "Delhi",        "India",         "Asia",           28.5799,  77.3299, "Vultr"],
  ["de-fra", "Frankfurt",    "Germany",       "Europe",         50.1109,   8.6820, "Vultr"],
  ["za-jnb", "Johannesburg", "South Africa",  "Africa",        -26.2023,  28.0436, "Vultr"],
  ["gb-lhr", "London",       "United Kingdom","Europe",         51.5085,  -0.1257, "Vultr"],
  ["us-lax", "Los Angeles",  "USA",           "North America",  34.0607,-118.2397, "Vultr"],
  ["es-mad", "Madrid",       "Spain",         "Europe",         40.4168,  -3.6847, "Vultr"],
  ["gb-man", "Manchester",   "United Kingdom","Europe",         55.7167,  -2.2667, "Vultr"],
  ["au-mel", "Melbourne",    "Australia",     "Oceania",       -37.8396, 144.9423, "Vultr"],
  ["mx-mex", "Mexico City",  "Mexico",        "North America",  19.4285, -99.1276, "Vultr"],
  ["us-mia", "Miami",        "USA",           "North America",  25.8118, -80.2364, "Vultr"],
  ["in-bom", "Mumbai",       "India",         "Asia",           19.0760,  72.8774, "Vultr"],
  ["us-ewr", "Newark",       "USA",           "North America",  40.5545, -74.4602, "Vultr"],
  ["jp-itm", "Osaka",        "Japan",         "Asia",           34.6942, 135.5022, "Vultr"],
  ["fr-cdg", "Paris",        "France",        "Europe",         48.9165,   2.3843, "Vultr"],
  ["cl-scl", "Santiago",     "Chile",         "South America", -33.4265, -70.5665, "Vultr"],
  ["us-sea", "Seattle",      "USA",           "North America",  47.3809,-122.2348, "Vultr"],
  ["kr-icn", "Seoul",        "South Korea",   "Asia",           37.5663, 126.9772, "Vultr"],
  ["us-sjc", "San Jose",     "USA",           "North America",  37.3541,-121.9555, "Vultr"],
  ["sg-sgp", "Singapore",    "Singapore",     "Asia",            1.2900, 103.8503, "Vultr"],
  ["se-sto", "Stockholm",    "Sweden",        "Europe",         59.3812,  17.9003, "Vultr"],
  ["au-syd", "Sydney",       "Australia",     "Oceania",       -33.9022, 151.2003, "Vultr"],
  ["il-tlv", "Tel Aviv",     "Israel",        "Asia",           32.1142,  34.9739, "Vultr"],
  ["jp-nrt", "Tokyo",        "Japan",         "Asia",           35.6895, 139.6923, "Vultr"],
  ["ca-yto", "Toronto",      "Canada",        "North America",  43.6537, -79.3829, "Vultr"],
  ["pl-waw", "Warsaw",       "Poland",        "Europe",         52.2298,  21.0118, "Vultr"],
  ["us-atl", "Atlanta",      "USA",           "North America",  33.7884, -84.4433, "Melbicom"],
  ["es-mad", "Madrid",       "Spain",         "Europe",         40.4168,  -3.6847, "Melbicom"],
  ["se-sto", "Stockholm",    "Sweden",        "Europe",         59.3812,  17.9003, "Melbicom"],
  ["in-mum", "Mumbai",       "India",         "Asia",           19.0760,  72.8774, "Melbicom"],
  ["sn-sin", "Singapore",    "Singapore",     "Asia",            1.2900, 103.8503, "Melbicom"],
  ["us-lax", "Los Angeles",  "USA",           "North America",  34.0607,-118.2397, "Melbicom"],
  ["ua-fuj", "Fujairah",     "UAE",           "Asia",           25.1164,  56.3414, "Melbicom"],
  ["ni-lag", "Lagos",        "Nigeria",       "Africa",          6.4530,   3.3958, "Melbicom"],
  ["fr-par", "Paris",        "France",        "Europe",         48.9165,   2.3843, "Melbicom"],
  ["bu-sof", "Sofia",        "Bulgaria",      "Europe",         42.6975,  23.3242, "Melbicom"],
  ["it-pal", "Palermo",      "Italy",         "Europe",         38.1158,  13.3597, "Melbicom"],
  ["li-vil", "Vilnius",      "Lithuania",     "Europe",         54.6892,  25.2800, "Melbicom"],
  ["la-rig", "Riga",         "Latvia",        "Europe",         56.9460,  24.1059, "Melbicom"],
  ["de-fra", "Frankfurt",    "Germany",       "Europe",         50.1109,   8.6820, "Melbicom"],
  ["ru-mos", "Moscow",       "Russia",        "Europe",         55.7523,  37.6155, "Melbicom"],
  ["nl-ams", "Amsterdam",    "Netherlands",   "Europe",         52.3785,   4.8998, "Melbicom"]
];

// --- Detect dual-provider cities (same lat/lon in both Vultr and Melbicom) ---
function coordKey(s) { return s[4].toFixed(4) + ',' + s[5].toFixed(4); }
var coordProviders = {};
vpSites.forEach(function(s) {
  var k = coordKey(s);
  if (!coordProviders[k]) coordProviders[k] = [];
  if (coordProviders[k].indexOf(s[6]) === -1) coordProviders[k].push(s[6]);
});

// --- Map ---
var map = L.map('testbed-map').setView([20, 10], 2);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
  maxZoom: 18
}).addTo(map);

var styleVultr   = {radius:7, fillColor:'#007bff', color:'#0056b3', weight:1, opacity:1, fillOpacity:.85};
var styleMelbi   = {radius:7, fillColor:'#e67e22', color:'#b35700', weight:1, opacity:1, fillOpacity:.85};
var styleBoth    = {radius:7, fillColor:'#6f42c1', color:'#4a2880', weight:1, opacity:1, fillOpacity:.85};
var styleHighlit = {radius:9, fillColor:'#ffc107', color:'#856404', weight:2, opacity:1, fillOpacity:1};

// One marker per unique lat/lon; dual-provider coords get purple marker
var markerByCoord = {};
var vpMarkers = vpSites.map(function(s, i) {
  var k = coordKey(s);
  if (!markerByCoord[k]) {
    var isDual = coordProviders[k].length > 1;
    var style  = isDual ? styleBoth : (s[6] === 'Vultr' ? styleVultr : styleMelbi);
    var provLabel = isDual ? 'Vultr + Melbicom' : s[6];
    var m = L.circleMarker([s[4], s[5]], style).addTo(map);
    m.bindPopup('<b>' + s[1] + ', ' + s[2] + '</b><br>' + s[0] + ' &mdash; ' + provLabel);
    m._vpOrigStyle = style;
    markerByCoord[k] = m;
  }
  return markerByCoord[k];
});

var legend = L.control({position:'bottomright'});
legend.onAdd = function() {
  var d = L.DomUtil.create('div','');
  d.style.cssText = 'background:white;padding:8px 12px;border-radius:4px;border:1px solid #ccc;font-size:13px;line-height:1.9;';
  d.innerHTML =
    '<span style="display:inline-block;width:12px;height:12px;border-radius:50%;background:#007bff;margin-right:6px;vertical-align:middle;"></span>Vultr<br>' +
    '<span style="display:inline-block;width:12px;height:12px;border-radius:50%;background:#e67e22;margin-right:6px;vertical-align:middle;"></span>Melbicom<br>' +
    '<span style="display:inline-block;width:12px;height:12px;border-radius:50%;background:#6f42c1;margin-right:6px;vertical-align:middle;"></span>Vultr + Melbicom';
  return d;
};
legend.addTo(map);

// --- Table ---
var vpSortCol = -1, vpSortAsc = true;
var vpSelectedRow = null, vpSelectedMarker = null;

function vpRender(data) {
  var tbody = document.getElementById('vp-tbody');
  tbody.innerHTML = '';
  data.forEach(function(s, i) {
    var tr = document.createElement('tr');
    tr.dataset.idx = s._origIdx;
    var isDual = coordProviders[coordKey(s)].length > 1;
    var badge = isDual
      ? '<span class="badge-both">Vultr + Melbicom</span>'
      : (s[6] === 'Vultr'
          ? '<span class="badge-vultr">Vultr</span>'
          : '<span class="badge-melbicom">Melbicom</span>');
    tr.innerHTML =
      '<td>' + s[0] + '</td>' +
      '<td>' + s[1] + '</td>' +
      '<td>' + s[2] + '</td>' +
      '<td>' + s[3] + '</td>' +
      '<td>' + badge + '</td>';
    tr.addEventListener('click', function() { vpRowClick(this); });
    tbody.appendChild(tr);
  });
}

function vpRowClick(tr) {
  // unhighlight previous
  if (vpSelectedRow) vpSelectedRow.classList.remove('vp-selected');
  if (vpSelectedMarker) vpSelectedMarker.setStyle(vpSelectedMarker._vpOrigStyle);

  vpSelectedRow = tr;
  tr.classList.add('vp-selected');
  tr.scrollIntoView({block:'nearest', behavior:'smooth'});

  var idx = parseInt(tr.dataset.idx);
  var marker = vpMarkers[idx];
  vpSelectedMarker = marker;
  marker.setStyle(styleHighlit);
  map.setView(marker.getLatLng(), Math.max(map.getZoom(), 4), {animate: true});
  marker.openPopup();
}

function vpSort(col) {
  if (vpSortCol === col) { vpSortAsc = !vpSortAsc; }
  else { vpSortCol = col; vpSortAsc = true; }

  // update arrows
  for (var i = 0; i < 7; i++) {
    var el = document.getElementById('vp-arr-' + i);
    el.textContent = i === col ? (vpSortAsc ? ' ▲' : ' ▼') : '';
  }

  var sorted = vpSites.map(function(s, i) {
    var copy = s.slice(); copy._origIdx = i; return copy;
  }).sort(function(a, b) {
    var va = a[col], vb = b[col];
    if (typeof va === 'number') return vpSortAsc ? va - vb : vb - va;
    return vpSortAsc ? String(va).localeCompare(String(vb)) : String(vb).localeCompare(String(va));
  });
  vpRender(sorted);
}

// Initial render
(function() {
  var initial = vpSites.map(function(s, i) { var c = s.slice(); c._origIdx = i; return c; });
  vpRender(initial);
})();
</script>

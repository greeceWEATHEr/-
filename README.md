
<html lang="el">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
}

body{
    font-family:Arial,Helvetica,sans-serif;
    background:
        linear-gradient(180deg,#061a36 0%,#0a2850 45%,#071b38 100%);
    color:white;
    min-height:100vh;
}

header{
    text-align:center;
    padding:28px 15px 20px;
    background:linear-gradient(180deg,#08244b,#0b3263);
    border-bottom:1px solid rgba(255,255,255,.12);
}

header h1{
    font-size:32px;
    margin-bottom:7px;
}

header p{
    color:#b9d5f5;
    font-size:15px;
}

.search-box{
    max-width:700px;
    margin:22px auto;
    display:flex;
    gap:10px;
    padding:0 15px;
}

.search-box input{
    flex:1;
    padding:15px 17px;
    border:none;
    border-radius:14px;
    outline:none;
    font-size:16px;
    background:#f4f8ff;
    color:#10233d;
}

.search-box button{
    padding:0 22px;
    border:none;
    border-radius:14px;
    background:#1687ff;
    color:white;
    font-size:16px;
    font-weight:bold;
    cursor:pointer;
}

.search-box button:hover{
    background:#0876e8;
}

.container{
    width:min(1500px,96%);
    margin:auto;
}

.current{
    margin:20px 0;
    padding:22px;
    border-radius:22px;
    background:
        linear-gradient(135deg,
        rgba(25,110,205,.5),
        rgba(9,39,80,.9));
    border:1px solid rgba(255,255,255,.12);
    box-shadow:0 12px 35px rgba(0,0,0,.25);
}

.location{
    text-align:center;
}

.location h2{
    font-size:29px;
    margin-bottom:5px;
}

.country{
    color:#c8def7;
    font-size:16px;
    margin-bottom:15px;
}

.current-main{
    display:flex;
    justify-content:center;
    align-items:center;
    gap:20px;
    flex-wrap:wrap;
}

.current-icon{
    font-size:65px;
}

.current-temp{
    font-size:52px;
    font-weight:bold;
}

.current-desc{
    color:#c9def5;
    font-size:17px;
}

.current-details{
    margin-top:20px;
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:10px;
}

.detail{
    background:rgba(255,255,255,.08);
    border-radius:13px;
    padding:13px;
    text-align:center;
    color:#dbeafe;
}

.detail strong{
    display:block;
    color:white;
    font-size:16px;
    margin-top:5px;
}

.section-title{
    font-size:22px;
    margin:28px 0 15px;
}

.forecast-grid{
    display:grid;
    grid-template-columns:repeat(6,1fr);
    gap:12px;
}

.day-card{
    background:
        linear-gradient(180deg,
        rgba(19,76,140,.92),
        rgba(7,34,69,.96));
    border:1px solid rgba(255,255,255,.1);
    border-radius:18px;
    padding:14px 10px;
    text-align:center;
    cursor:pointer;
    transition:.2s;
    min-width:0;
}

.day-card:hover{
    transform:translateY(-3px);
    background:
        linear-gradient(180deg,
        rgba(27,100,181,.98),
        rgba(8,40,78,.98));
}

.day-name{
    font-size:17px;
    font-weight:bold;
}

.date{
    color:#bcd4ee;
    font-size:13px;
    margin-top:4px;
}

.day-icon{
    font-size:42px;
    margin:13px 0;
    min-height:48px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.temps{
    font-size:18px;
    font-weight:bold;
}

.min-temp{
    color:#9bc7ef;
    margin-left:5px;
}

.rain{
    margin-top:9px;
    color:#d7ebff;
    font-size:14px;
}

.wind{
    margin-top:7px;
    color:#b9d5f2;
    font-size:13px;
}

.hourly-box{
    margin:22px 0 30px;
    padding:18px;
    border-radius:20px;
    background:
        linear-gradient(135deg,
        rgba(10,57,108,.95),
        rgba(5,28,57,.98));
    border:1px solid rgba(255,255,255,.1);
    display:none;
}

.hourly-title{
    font-size:21px;
    margin-bottom:14px;
}

.hourly-scroll{
    display:flex;
    gap:10px;
    overflow-x:auto;
    padding-bottom:8px;
}

.hour{
    min-width:125px;
    background:rgba(255,255,255,.07);
    border-radius:15px;
    padding:12px;
    text-align:center;
}

.hour-time{
    font-weight:bold;
    margin-bottom:8px;
}

.hour-icon{
    font-size:32px;
    margin:6px 0;
}

.hour-temp{
    font-size:19px;
    font-weight:bold;
}

.hour-rain{
    margin-top:8px;
    color:#d7ebff;
}

.hour-wind{
    margin-top:7px;
    color:#bcd5ef;
    font-size:13px;
}

.loading{
    text-align:center;
    padding:30px;
    color:#c8def7;
    display:none;
}

.error{
    text-align:center;
    padding:25px;
    color:#ffb9b9;
    display:none;
}

footer{
    text-align:center;
    padding:30px 15px;
    color:#8eafd1;
    font-size:13px;
}

.night-moon{
    display:inline-block;
    width:40px;
    height:40px;
    border-radius:50%;
    background:#aab5c3;
    position:relative;
    box-shadow:0 0 10px rgba(180,195,210,.25);
}

.night-moon:after{
    content:"";
    position:absolute;
    width:40px;
    height:40px;
    border-radius:50%;
    background:#12345e;
    left:12px;
    top:-5px;
}

.night-cloud{
    position:relative;
    width:54px;
    height:45px;
}

.night-cloud .moon{
    position:absolute;
    left:4px;
    top:0;
}

.night-cloud .cloud{
    position:absolute;
    bottom:2px;
    right:0;
    width:38px;
    height:19px;
    background:#aab6c5;
    border-radius:20px;
}

.night-cloud .cloud:before,
.night-cloud .cloud:after{
    content:"";
    position:absolute;
    background:#aab6c5;
    border-radius:50%;
}

.night-cloud .cloud:before{
    width:20px;
    height:20px;
    left:7px;
    top:-10px;
}

.night-cloud .cloud:after{
    width:17px;
    height:17px;
    right:5px;
    top:-7px;
}

@media(max-width:1100px){
    .forecast-grid{
        grid-template-columns:repeat(4,1fr);
    }
}

@media(max-width:700px){
    header h1{
        font-size:26px;
    }

    .search-box{
        flex-direction:column;
    }

    .search-box button{
        padding:14px;
    }

    .current-details{
        grid-template-columns:repeat(2,1fr);
    }

    .forecast-grid{
        grid-template-columns:repeat(3,1fr);
        gap:8px;
    }

    .day-card{
        padding:11px 6px;
        border-radius:14px;
    }

    .day-name{
        font-size:14px;
    }

    .date{
        font-size:11px;
    }

    .day-icon{
        font-size:34px;
        margin:9px 0;
    }

    .temps{
        font-size:15px;
    }

    .rain,.wind{
        font-size:11px;
    }
}
</style>
</head>

<body>

<header>
    <h1>🇬🇷 Greece Weather</h1>
    <p>Πρόγνωση καιρού για όλη την Ελλάδα</p>
</header>

<div class="search-box">
    <input
        id="searchInput"
        type="text"
        value="Θεσσαλονίκη"
        placeholder="Γράψε πόλη ή περιοχή..."
    >
    <button onclick="searchLocation()">Αναζήτηση</button>
</div>

<div class="container">

    <div id="loading" class="loading">
        Φόρτωση δεδομένων καιρού...
    </div>

    <div id="error" class="error">
        Δεν ήταν δυνατή η φόρτωση δεδομένων καιρού.
    </div>

    <section id="weatherContent">

        <div class="current">

            <div class="location">
                <h2 id="locationName">Θεσσαλονίκη</h2>
                <div class="country" id="countryName">🇬🇷 Ελλάδα</div>
            </div>

            <div class="current-main">

                <div id="currentIcon" class="current-icon">
                    ☀️
                </div>

                <div>
                    <div id="currentTemp" class="current-temp">
                        --
                    </div>

                    <div id="currentDesc" class="current-desc">
                        --
                    </div>
                </div>

            </div>

            <div class="current-details">

                <div class="detail">
                    💧 Υγρασία
                    <strong id="humidity">--%</strong>
                </div>

                <div class="detail">
                    💨 Άνεμος
                    <strong id="currentWind">-- km/h</strong>
                </div>

                <div class="detail">
                    🧭 Διεύθυνση
                    <strong id="currentWindDir">--</strong>
                </div>

                <div class="detail">
                    ☔ Υετός
                    <strong id="currentRain">--%</strong>
                </div>

            </div>
        </div>

        <h2 class="section-title">
            📅 Πρόγνωση 15 ημερών
        </h2>

        <div id="forecastGrid" class="forecast-grid"></div>

        <div id="hourlyBox" class="hourly-box">
            <div id="hourlyTitle" class="hourly-title"></div>

            <div id="hourlyScroll" class="hourly-scroll"></div>
        </div>

    </section>
</div>

<footer>
    ECMWF IFS HRES • NOAA GFS • DWD ICON
</footer>

<script>

let locationData = null;

let weatherData = {
    ecmwf:null,
    gfs:null,
    icon:null
};

let selectedDay = 0;


/* =========================
   FLAGS
========================= */

function countryFlag(code){

    if(!code || code.length !== 2){
        return "🌍";
    }

    return code
        .toUpperCase()
        .split("")
        .map(c =>
            String.fromCodePoint(127397 + c.charCodeAt(0))
        )
        .join("");
}


/* =========================
   WEATHER DESCRIPTION
========================= */

function weatherDescription(code){

    const descriptions = {

        0:"Καθαρός ουρανός",

        1:"Κυρίως αίθριος",
        2:"Μερική συννεφιά",
        3:"Συννεφιασμένος",

        45:"Ομίχλη",
        48:"Παγωμένη ομίχλη",

        51:"Ψιλόβροχο",
        53:"Ψιλόβροχο",
        55:"Ψιλόβροχο",

        56:"Παγωμένο ψιλόβροχο",
        57:"Παγωμένο ψιλόβροχο",

        61:"Βροχή",
        63:"Βροχή",
        65:"Ισχυρή βροχή",

        66:"Παγωμένη βροχή",
        67:"Παγωμένη βροχή",

        71:"Χιονόπτωση",
        73:"Χιονόπτωση",
        75:"Ισχυρή χιονόπτωση",
        77:"Χιονοκόκκοι",

        80:"Μπόρες",
        81:"Μπόρες",
        82:"Ισχυρές μπόρες",

        85:"Χιονομπόρες",
        86:"Ισχυρές χιονομπόρες",

        95:"Καταιγίδα",
        96:"Καταιγίδα με χαλάζι",
        99:"Ισχυρή καταιγίδα με χαλάζι"
    };

    return descriptions[code] || "Άγνωστη κατάσταση";
}


/* =========================
   WEATHER ICON
========================= */

function weatherIcon(
    code,
    isDay,
    precipitationProbability = 0,
    snowfall = 0
){

    /*
       ΚΑΤΩ ΑΠΟ 30%
       Δεν χρησιμοποιούμε emoji υετού.
    */

    if(precipitationProbability < 30){

        if(!isDay){

            if(code === 2 || code === 3){

                return `
                    <div class="night-cloud">
                        <span class="night-moon moon"></span>
                        <span class="cloud"></span>
                    </div>
                `;

            }

            return `
                <span class="night-moon"></span>
            `;
        }

        if(code === 0){
            return "☀️";
        }

        if(code === 1){
            return "🌤️";
        }

        if(code === 2){
            return "⛅";
        }

        if(code === 3){
            return "☁️";
        }

        if(code === 45 || code === 48){
            return "🌫️";
        }

        return "☁️";
    }


    /*
       30% ΚΑΙ ΠΑΝΩ
       Πρέπει να εμφανίζεται emoji υετού.
    */

    if(
        code === 95 ||
        code === 96 ||
        code === 99
    ){
        return "⛈️";
    }


    if(
        code === 71 ||
        code === 73 ||
        code === 75 ||
        code === 77 ||
        code === 85 ||
        code === 86 ||
        snowfall > 0
    ){
        return "🌨️";
    }


    if(
        code === 51 ||
        code === 53 ||
        code === 55 ||
        code === 56 ||
        code === 57 ||
        code === 61 ||
        code === 63 ||
        code === 65 ||
        code === 66 ||
        code === 67 ||
        code === 80 ||
        code === 81 ||
        code === 82
    ){
        return "🌧️";
    }


    return "🌧️";
}


/* =========================
   WIND DIRECTION
========================= */

function windDirection(degrees){

    const directions = [
        "Β",
        "ΒΒΑ",
        "ΒΑ",
        "ΑΒΑ",
        "Α",
        "ΑΝΑ",
        "ΝΑ",
        "ΝΝΑ",
        "Ν",
        "ΝΝΔ",
        "ΝΔ",
        "ΔΝΔ",
        "Δ",
        "ΔΒΔ",
        "ΒΔ",
        "ΒΒΔ"
    ];

    const index =
        Math.round(degrees / 22.5) % 16;

    return directions[index];
}


/* =========================
   SEARCH LOCATION
========================= */

async function searchLocation(){

    const input =
        document.getElementById("searchInput").value.trim();

    if(!input){
        return;
    }

    document.getElementById("loading").style.display = "block";
    document.getElementById("error").style.display = "none";
    document.getElementById("weatherContent").style.display = "none";

    try{

        const url =
            "https://geocoding-api.open-meteo.com/v1/search?" +
            "name=" + encodeURIComponent(input) +
            "&count=1" +
            "&language=el" +
            "&format=json";

        const response = await fetch(url);

        if(!response.ok){
            throw new Error("Geocoding error");
        }

        const data = await response.json();

        if(!data.results || !data.results.length){
            throw new Error("Location not found");
        }

        const result = data.results[0];

        locationData = {
            name: result.name,
            latitude: result.latitude,
            longitude: result.longitude,
            country: result.country || "",
            countryCode: result.country_code || ""
        };

        await loadWeather();

    }catch(error){

        console.error(error);

        document.getElementById("loading").style.display = "none";
        document.getElementById("weatherContent").style.display = "none";
        document.getElementById("error").style.display = "block";
    }
}


/* =========================
   LOAD WEATHER
========================= */

async function loadWeather(){

    const lat = locationData.latitude;
    const lon = locationData.longitude;

    const base =
        "https://api.open-meteo.com/v1/forecast?";

    const common =
        "latitude=" + lat +
        "&longitude=" + lon +
        "&forecast_days=15" +
        "&timezone=auto" +

        "&current=" +
        "temperature_2m," +
        "relative_humidity_2m," +
        "apparent_temperature," +
        "weather_code," +
        "wind_speed_10m," +
        "wind_direction_10m," +
        "precipitation," +
        "precipitation_probability" +

        "&hourly=" +
        "temperature_2m," +
        "weather_code," +
        "precipitation_probability," +
        "precipitation," +
        "snowfall," +
        "wind_speed_10m," +
        "wind_direction_10m," +
        "is_day" +

        "&daily=" +
        "weather_code," +
        "temperature_2m_max," +
        "temperature_2m_min," +
        "precipitation_probability_max," +
        "precipitation_sum," +
        "snowfall_sum," +
        "wind_speed_10m_max," +
        "wind_direction_10m_dominant," +
        "sunrise," +
        "sunset";


    const urls = {

        ecmwf:
            base +
            common +
            "&models=ecmwf_ifs025",

        gfs:
            base +
            common +
            "&models=gfs_global",

        icon:
            base +
            common +
            "&models=icon_seamless"
    };


    try{

        const [
            ecmwfResponse,
            gfsResponse,
            iconResponse
        ] = await Promise.all([

            fetch(urls.ecmwf),
            fetch(urls.gfs),
            fetch(urls.icon)

        ]);


        if(
            !ecmwfResponse.ok ||
            !gfsResponse.ok ||
            !iconResponse.ok
        ){
            throw new Error("Weather API error");
        }


        weatherData.ecmwf =
            await ecmwfResponse.json();

        weatherData.gfs =
            await gfsResponse.json();

        weatherData.icon =
            await iconResponse.json();


        displayWeather();

    }catch(error){

        console.error(error);

        document.getElementById("loading").style.display = "none";
        document.getElementById("weatherContent").style.display = "none";
        document.getElementById("error").style.display = "block";
    }
}


/* =========================
   DISPLAY WEATHER
========================= */

function displayWeather(){

    const d = weatherData.ecmwf;

    document.getElementById("locationName").textContent =
        locationData.name;

    document.getElementById("countryName").textContent =
        countryFlag(locationData.countryCode) +
        " " +
        locationData.country;


    const currentCode =
        d.current.weather_code;

    const currentTemp =
        d.current.temperature_2m;

    const currentProbability =
        d.current.precipitation_probability || 0;


    document.getElementById("currentIcon").innerHTML =
        weatherIcon(
            currentCode,
            true,
            currentProbability,
            0
        );


    document.getElementById("currentTemp").textContent =
        Math.round(currentTemp) + "°C";


    document.getElementById("currentDesc").textContent =
        weatherDescription(currentCode);


    document.getElementById("humidity").textContent =
        d.current.relative_humidity_2m + "%";


    document.getElementById("currentWind").textContent =
        Math.round(d.current.wind_speed_10m) +
        " km/h";


    document.getElementById("currentWindDir").textContent =
        windDirection(d.current.wind_direction_10m);


    document.getElementById("currentRain").textContent =
        currentProbability + "%";


    displayForecast();


    document.getElementById("loading").style.display = "none";
    document.getElementById("error").style.display = "none";
    document.getElementById("weatherContent").style.display = "block";
}


/* =========================
   DISPLAY 15 DAYS
========================= */

function displayForecast(){

    const d = weatherData.ecmwf;

    const grid =
        document.getElementById("forecastGrid");

    grid.innerHTML = "";


    for(let i = 0; i < 15; i++){

        const date =
            new Date(
                d.daily.time[i] + "T12:00:00"
            );


        const dayName =
            date.toLocaleDateString(
                "el-GR",
                {
                    weekday:"short"
                }
            );


        const dateText =
            date.toLocaleDateString(
                "el-GR",
                {
                    day:"2-digit",
                    month:"2-digit"
                }
            );


        const code =
            d.daily.weather_code[i];


        const max =
            Math.round(
                d.daily.temperature_2m_max[i]
            );


        const min =
            Math.round(
                d.daily.temperature_2m_min[i]
            );


        const rain =
            d.daily.precipitation_probability_max[i] || 0;


        const snowfall =
            d.daily.snowfall_sum[i] || 0;


        const wind =
            Math.round(
                d.daily.wind_speed_10m_max[i]
            );


        const windDir =
            windDirection(
                d.daily.wind_direction_10m_dominant[i]
            );


        /*
           Για την ημερήσια κάρτα
           θεωρούμε ημέρα.
        */

        const icon =
            weatherIcon(
                code,
                true,
                rain,
                snowfall
            );


        const card =
            document.createElement("div");

        card.className = "day-card";

        card.onclick = () => {
            showHourly(i);
        };


        card.innerHTML = `

            <div class="day-name">
                ${dayName}
            </div>

            <div class="date">
                ${dateText}
            </div>

            <div class="day-icon">
                ${icon}
            </div>

            <div class="temps">
                ${max}°C
                <span class="min-temp">
                    ${min}°
                </span>
            </div>

            <div class="rain">
                💧 ${rain}%
            </div>

            <div class="wind">
                💨 ${wind} km/h ${windDir}
            </div>
        `;


        grid.appendChild(card);
    }
}


/* =========================
   HOURLY FORECAST
========================= */

function showHourly(dayIndex){

    selectedDay = dayIndex;

    const d = weatherData.ecmwf;

    const date =
        d.daily.time[dayIndex];


    const dateObject =
        new Date(date + "T12:00:00");


    const dateText =
        dateObject.toLocaleDateString(
            "el-GR",
            {
                weekday:"long",
                day:"numeric",
                month:"long"
            }
        );


    document.getElementById("hourlyTitle").textContent =
        "🕐 Ωριαία πρόγνωση — " + dateText;


    const box =
        document.getElementById("hourlyBox");


    const scroll =
        document.getElementById("hourlyScroll");


    scroll.innerHTML = "";


    /*
       Βρίσκουμε όλες τις ώρες
       που ανήκουν στη συγκεκριμένη ημέρα.
    */

    for(let i = 0; i < d.hourly.time.length; i++){

        const time =
            d.hourly.time[i];


        if(!time.startsWith(date)){
            continue;
        }


        const dateTime =
            new Date(time);


        const hour =
            dateTime.getHours();


        const temp =
            Math.round(
                d.hourly.temperature_2m[i]
            );


        const code =
            d.hourly.weather_code[i];


        const rain =
            d.hourly.precipitation_probability[i] || 0;


        const snowfall =
            d.hourly.snowfall[i] || 0;


        const wind =
            Math.round(
                d.hourly.wind_speed_10m[i]
            );


        const windDir =
            windDirection(
                d.hourly.wind_direction_10m[i]
            );


        const isDay =
            d.hourly.is_day[i] === 1;


        const icon =
            weatherIcon(
                code,
                isDay,
                rain,
                snowfall
            );


        /*
           ΩΡΙΑΙΑ ΠΡΟΒΛΕΨΗ ΥΕΤΟΥ

           Πάντα ξεκινάμε με 💧.

           Γίνεται ❄️ μόνο όταν:
           1. ο κωδικός καιρού δείχνει χιόνι
              ή
           2. η θερμοκρασία είναι ≤ 0°C.

           Δεν εμφανίζουμε mm ή cm.
        */

        let precipitationHTML = "";

        const hourlyCode =
            d.hourly.weather_code[i];


        const hasSnowEmoji =
            [
                71,
                73,
                75,
                77,
                85,
                86
            ].includes(hourlyCode);


        const isSnow =
            hasSnowEmoji ||
            temp <= 0;


        if(isSnow){

            precipitationHTML = `
                ❄️ ${rain}%
            `;

        }else{

            precipitationHTML = `
                💧 ${rain}%
            `;

        }


        const hourCard =
            document.createElement("div");

        hourCard.className = "hour";


        hourCard.innerHTML = `

            <div class="hour-time">
                ${String(hour).padStart(2,"0")}:00
            </div>

            <div class="hour-icon">
                ${icon}
            </div>

            <div class="hour-temp">
                ${temp}°C
            </div>

            <div class="hour-rain">
                ${precipitationHTML}
            </div>

            <div class="hour-wind">
                💨 ${wind} km/h ${windDir}
            </div>

        `;


        scroll.appendChild(hourCard);
    }


    box.style.display = "block";


    /*
       Μετάβαση στο hourly section
    */

    setTimeout(() => {

        box.scrollIntoView({
            behavior:"smooth",
            block:"start"
        });

    },50);
}


/* =========================
   ENTER SEARCH
========================= */

document
    .getElementById("searchInput")
    .addEventListener(
        "keydown",
        function(event){

            if(event.key === "Enter"){
                searchLocation();
            }

        }
    );


/* =========================
   INITIAL LOCATION
========================= */

searchLocation();

</script>

</body>

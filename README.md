<!DOCTYPE html>
<html lang="el">

<head>

<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0">

<title>Greece Weather</title>


<style>

*{
    box-sizing:border-box;
}

body{
    margin:0;
    font-family:
        Arial,
        Helvetica,
        sans-serif;
    color:#fff;
    background:
        linear-gradient(
            180deg,
            #071d35,
            #0d3762
        );
}

.container{
    width:min(100%,960px);
    margin:auto;
    padding:16px;
}


/* =====================================
   HEADER
===================================== */

.header{
    position:relative;
    background:
        rgba(3,20,38,.72);
    padding:28px 60px 28px 20px;
    text-align:center;
    margin-bottom:25px;
}

.header h1{
    margin:0;
    font-size:30px;
}

.header p{
    margin:18px 0 0;
    color:#d6dce4;
    font-size:16px;
}


/* =====================================
   MENU
===================================== */

.menu-button{
    position:absolute;
    top:18px;
    right:18px;
    width:43px;
    height:43px;
    border:0;
    border-radius:12px;
    background:rgba(255,255,255,.12);
    color:#fff;
    font-size:25px;
    cursor:pointer;
    display:flex;
    align-items:center;
    justify-content:center;
    transition:.18s;
}

.menu-button:hover{
    background:rgba(255,255,255,.22);
}

.menu{
    display:none;
    position:absolute;
    top:68px;
    right:18px;
    width:270px;
    max-height:70vh;
    overflow-y:auto;
    background:rgba(5,27,50,.97);
    border:1px solid rgba(255,255,255,.18);
    border-radius:15px;
    padding:8px;
    z-index:1000;
    box-shadow:0 10px 30px rgba(0,0,0,.35);
}

.menu.open{
    display:block;
}

.menu-item{
    width:100%;
    border:0;
    background:transparent;
    color:#fff;
    text-align:left;
    padding:13px 12px;
    border-radius:10px;
    font-size:14px;
    cursor:pointer;
}

.menu-item:hover{
    background:rgba(255,255,255,.12);
}


/* =====================================
   SEARCH
===================================== */

.search{
    display:flex;
    gap:10px;
    margin-bottom:25px;
}

.search input{
    flex:1;
    border:0;
    outline:0;
    border-radius:15px;
    padding:17px;
    font-size:16px;
}

.search button{
    border:0;
    border-radius:15px;
    padding:0 22px;
    font-weight:bold;
    font-size:15px;
    cursor:pointer;
}


/* =====================================
   CURRENT WEATHER
===================================== */

.current{
    background:
        rgba(57,85,117,.72);
    border-radius:20px;
    padding:25px;
    text-align:center;
    margin-bottom:25px;
}

.current h2{
    margin:0 0 20px;
    font-size:26px;
}

.temperature{
    font-size:60px;
    font-weight:300;
    margin-bottom:15px;
}

.condition{
    font-size:17px;
    margin-bottom:24px;
}

.current-grid{
    display:grid;
    grid-template-columns:
        repeat(3,1fr);
    gap:12px;
}

.current-box{
    background:
        rgba(104,133,165,.48);
    border-radius:14px;
    padding:16px 8px;
}

.current-box span{
    display:block;
    color:#e0e5ea;
    margin-bottom:5px;
}

.current-box strong{
    font-size:15px;
}


/* =====================================
   SECTION TITLE
===================================== */

.section-title{
    display:flex;
    align-items:center;
    gap:8px;
    font-size:24px;
    font-weight:bold;
    border-bottom:
        2px solid
        rgba(255,255,255,.55);
    padding-bottom:12px;
    margin-bottom:15px;
}


/* =====================================
   15 ΗΜΕΡΕΣ
===================================== */

.forecast{
    display:grid;
    grid-template-columns:
        repeat(6,1fr);
    gap:12px;
}

.day{
    background:
        rgba(53,84,119,.78);
    border-radius:17px;
    padding:18px 8px;
    text-align:center;
    cursor:pointer;
    transition:.18s;
    border:
        1px solid
        transparent;
}

.day:hover{
    transform:
        translateY(-3px);
    background:
        rgba(72,105,143,.95);
    border-color:
        rgba(255,255,255,.25);
}

.day:active{
    transform:
        scale(.97);
}

.day-name{
    font-weight:bold;
    font-size:15px;
}

.date{
    margin-top:9px;
    color:#e1e5e9;
    font-size:14px;
}

.icon{
    font-size:35px;
    margin:18px 0 12px;
    height:40px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.max{
    font-size:17px;
    font-weight:bold;
}

.min{
    margin-top:6px;
    color:#d0d7df;
}

.rain{
    margin-top:10px;
    font-size:12px;
    color:#c9e9ff;
}


/* =====================================
   ΝΥΧΤΕΡΙΝΑ ΕΙΚΟΝΙΔΙΑ
===================================== */

.night-moon{
    display:inline-block;
    filter:
        grayscale(1)
        brightness(.78)
        sepia(.10)
        hue-rotate(175deg);
    opacity:.90;
}

.night-partly-cloudy{
    width:38px;
    height:38px;
    display:inline-block;
    vertical-align:middle;
    background:
        url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Ccircle cx='25' cy='23' r='15' fill='%2395a9bd'/%3E%3Cpath d='M15 42c0-6.5 5.3-11.8 11.8-11.8 4.3 0 8.1 2.3 10.1 5.8 1.1-.4 2.3-.6 3.5-.6 6.3 0 11.4 5.1 11.4 11.4H15.8C15.3 45.6 15 43.8 15 42z' fill='%23c7d0d9'/%3E%3Cpath d='M20 38c1.5-4.6 5.8-7.9 10.9-7.9 4.1 0 7.7 2.1 9.8 5.3' fill='none' stroke='%23e2e7eb' stroke-width='2' stroke-linecap='round'/%3E%3C/svg%3E")
        center/
        contain
        no-repeat;
}


/* =====================================
   ΩΡΙΑΙΑ ΠΡΟΓΝΩΣΗ
===================================== */

.hourly-section{
    display:none;
    margin-top:28px;
    background:
        rgba(5,27,50,.72);
    border-radius:20px;
    padding:20px;
}

.hourly-header{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:10px;
    border-bottom:
        1px solid
        rgba(255,255,255,.3);
    padding-bottom:15px;
    margin-bottom:15px;
}

.hourly-header h3{
    margin:0;
    font-size:21px;
}

.close-hourly{
    background:
        rgba(255,255,255,.15);
    border:0;
    color:white;
    border-radius:10px;
    padding:8px 13px;
    cursor:pointer;
}


/* =====================================
   ΩΡΕΣ
===================================== */

.hourly{
    display:grid;
    gap:8px;
}

.hour{
    display:grid;
    grid-template-columns:
        70px
        50px
        1fr
        1fr
        1fr
        1fr;
    align-items:center;
    background:
        rgba(65,96,130,.62);
    border-radius:12px;
    padding:12px 10px;
    gap:8px;
}

.hour-time{
    font-weight:bold;
}

.hour-icon{
    font-size:25px;
    text-align:center;
    height:32px;
    display:flex;
    align-items:center;
    justify-content:center;
}

.hour-data{
    font-size:13px;
    color:#e4e8ed;
    line-height:1.5;
}


/* =====================================
   ΙΣΤΟΡΙΚΟ
===================================== */

.history-section{
    display:none;
    margin-top:28px;
    background:
        rgba(5,27,50,.72);
    border-radius:20px;
    padding:20px;
}

.history-header{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:10px;
    border-bottom:
        1px solid
        rgba(255,255,255,.3);
    padding-bottom:15px;
    margin-bottom:15px;
}

.history-header h3{
    margin:0;
    font-size:21px;
}

.close-history{
    background:
        rgba(255,255,255,.15);
    border:0;
    color:white;
    border-radius:10px;
    padding:8px 13px;
    cursor:pointer;
}

.history{
    display:grid;
    gap:9px;
}


/* =====================================
   ΕΠΙΛΟΓΗ 1-10 ΕΤΩΝ
===================================== */

.history-range-title{
    margin:0 0 14px;
    color:#dce5ee;
    font-size:15px;
    text-align:center;
}

.history-ranges{
    display:grid;
    grid-template-columns:
        repeat(5,1fr);
    gap:10px;
}

.history-range-button{
    border:0;
    color:#fff;
    background:
        rgba(65,96,130,.72);
    border-radius:14px;
    padding:15px 8px;
    font-size:14px;
    font-weight:bold;
    cursor:pointer;
    transition:.18s;
}

.history-range-button:hover{
    background:
        rgba(72,105,143,.95);
    transform:
        translateY(-2px);
}


/* =====================================
   ΙΣΤΟΡΙΚΟ ΕΤΩΝ
===================================== */

.history-years{
    display:grid;
    grid-template-columns:
        repeat(2,1fr);
    gap:12px;
}

.history-year-button,
.history-month-button,
.history-back-button{
    border:0;
    color:#fff;
    background:
        rgba(65,96,130,.72);
    border-radius:14px;
    padding:17px 12px;
    font-size:15px;
    font-weight:bold;
    cursor:pointer;
    transition:.18s;
}

.history-year-button:hover,
.history-month-button:hover,
.history-back-button:hover{
    background:
        rgba(72,105,143,.95);
    transform:
        translateY(-2px);
}

.history-months{
    display:grid;
    grid-template-columns:
        repeat(3,1fr);
    gap:10px;
}

.history-navigation{
    display:flex;
    gap:10px;
    margin-bottom:15px;
    flex-wrap:wrap;
}

.history-back-button{
    padding:10px 14px;
    font-size:14px;
}


/* =====================================
   ΗΜΕΡΕΣ ΙΣΤΟΡΙΚΟΥ
===================================== */

.history-days{
    display:grid;
    grid-template-columns:
        repeat(6,minmax(0,1fr));
    gap:10px;
}


/* =====================================
   ΙΣΤΟΡΙΚΟ ΚΟΥΤΑΚΙ
===================================== */

.history-day{
    display:flex;
    flex-direction:column;
    align-items:center;
    justify-content:flex-start;

    width:100%;
    min-width:0;
    min-height:136px;

    background:
        rgba(65,96,130,.62);

    border-radius:13px;

    padding:12px 8px;

    cursor:pointer;

    transition:.18s;

    border:
        1px solid
        transparent;
}

.history-day:hover{
    background:
        rgba(72,105,143,.90);

    border-color:
        rgba(255,255,255,.20);

    transform:
        translateY(-2px);
}

.history-day:active{
    transform:
        scale(.98);
}


/* =====================================
   ΗΜΕΡΟΜΗΝΙΑ
===================================== */

.history-date{
    width:100%;

    font-weight:bold;

    font-size:14px;

    text-align:center;

    white-space:nowrap;

    line-height:1.1;

    min-height:20px;

    display:flex;

    align-items:center;

    justify-content:center;

    margin-bottom:10px;
}


/* =====================================
   ΚΑΤΩ ΜΕΡΟΣ ΚΑΡΤΑΣ
===================================== */

.history-day-content{
    display:flex;

    align-items:center;

    justify-content:center;

    gap:10px;

    width:100%;

    flex:1;
}


/* =====================================
   ΘΕΡΜΟΚΡΑΣΙΕΣ ΙΣΤΟΡΙΚΟΥ
===================================== */

.history-temperature{
    display:flex;

    flex-direction:column;

    justify-content:center;

    align-items:center;

    gap:5px;

    font-size:13px;

    line-height:1.2;

    text-align:center;

    min-width:64px;
}

.history-temperature .day-temp{
    font-weight:bold;
    color:#fff;
    white-space:nowrap;
}

.history-temperature .night-temp{
    color:#d0d7df;
    white-space:nowrap;
}


/* =====================================
   ΘΕΡΜΟΜΕΤΡΟ
===================================== */

.history-thermometer{
    position:relative;

    width:18px;
    height:54px;

    flex:
        0 0 18px;
}

.history-thermometer::before{
    content:"";

    position:absolute;

    left:6px;
    top:1px;

    width:6px;
    height:39px;

    border-radius:6px;

    background:#f1f4f7;
}

.history-thermometer::after{
    content:"";

    position:absolute;

    left:1px;
    bottom:0;

    width:17px;
    height:17px;

    border-radius:50%;

    background:#f1f4f7;
}

.history-thermometer-fill{
    position:absolute;

    left:8px;
    bottom:8px;

    width:3px;
    height:31px;

    border-radius:3px;

    background:#e53935;

    z-index:2;
}

.history-thermometer-bulb{
    position:absolute;

    left:5px;
    bottom:3px;

    width:9px;
    height:9px;

    border-radius:50%;

    background:#e53935;

    z-index:2;
}


/* =====================================
   MODEL INFO
===================================== */

.model-info{
    margin-top:18px;
    color:#bdc9d6;
    font-size:12px;
    line-height:1.5;
}


/* =====================================
   LOADING
===================================== */

.loading{
    text-align:center;
    padding:30px;
    font-size:16px;
}


/* =====================================
   TABLET / MOBILE
===================================== */

@media(max-width:750px){

    .forecast{
        grid-template-columns:
            repeat(3,1fr);
    }

    .current-grid{
        grid-template-columns:
            1fr;
    }

    .hour{
        grid-template-columns:
            55px
            40px
            1fr
            1fr;
    }

    .hour-data:nth-child(5),
    .hour-data:nth-child(6){
        display:none;
    }

    .history-ranges{
        grid-template-columns:
            repeat(3,1fr);
    }

    .history-years{
        grid-template-columns:
            1fr;
    }

    .history-months{
        grid-template-columns:
            repeat(3,1fr);
    }

    .history-days{
        grid-template-columns:
            repeat(3,minmax(0,1fr));

        gap:8px;
    }

    .history-day{
        min-height:132px;
        padding:11px 6px;
    }

    .history-date{
        font-size:13px;
    }

    .history-temperature{
        font-size:11px;
        min-width:58px;
    }

    .history-day-content{
        gap:8px;
    }

}


@media(max-width:430px){

    .container{
        padding:12px;
    }

    .header h1{
        font-size:26px;
    }

    .temperature{
        font-size:52px;
    }

    .forecast{
        grid-template-columns:
            repeat(3,1fr);
        gap:9px;
    }

    .day{
        padding:15px 5px;
    }

    .icon{
        font-size:30px;
    }

    .menu{
        right:10px;
        width:225px;
    }

    .history-ranges{
        grid-template-columns:
            repeat(2,1fr);
    }

    .history-months{
        grid-template-columns:
            repeat(2,1fr);
    }

    .history-days{
        grid-template-columns:
            repeat(2,minmax(0,1fr));

        gap:7px;
    }

    .history-day{
        min-height:125px;

        border-radius:10px;

        padding:9px 5px;
    }

    .history-date{
        font-size:12px;
        margin-bottom:8px;
    }

    .history-temperature{
        font-size:10px;
        min-width:52px;
    }

    .history-day-content{
        gap:7px;
    }

    .history-thermometer{
        transform:scale(.9);
        transform-origin:center;
    }

}

</style>

</head>


<body>


<div class="container">


    <div class="header">

        <h1>
            🇬🇷 Greece Weather
        </h1>

        <p>
            Πρόγνωση καιρού για όλη την Ελλάδα
        </p>


        <button
            class="menu-button"
            onclick="toggleMenu()"
            aria-label="Μενού">

            ☰

        </button>


        <div
            id="menu"
            class="menu">

            <button
                class="menu-item"
                onclick="openHistorySelector()">

                📜 Ιστορικό τελευταίων 1–10 ετών

            </button>

        </div>

    </div>


    <div class="search">

        <input
            id="cityInput"
            placeholder="Γράψε πόλη..."
            value="Θεσσαλονίκη"
        >

        <button
            onclick="searchCity()">

            Αναζήτηση

        </button>

    </div>


    <div id="current"></div>


    <div class="section-title">

        📅 Πρόγνωση 15 ημερών

    </div>


    <div
        id="forecast"
        class="forecast">

        <div class="loading">

            Φόρτωση πρόγνωσης...

        </div>

    </div>


    <div
        id="hourlySection"
        class="hourly-section">

        <div class="hourly-header">

            <h3 id="hourlyTitle"></h3>

            <button
                class="close-hourly"
                onclick="closeHourly()">

                ✕ Κλείσιμο

            </button>

        </div>

        <div
            id="hourly"
            class="hourly">
        </div>

    </div>


    <div
        id="historySection"
        class="history-section">

        <div class="history-header">

            <h3 id="historyTitle">
                📜 Ιστορικό καιρού
            </h3>

            <button
                class="close-history"
                onclick="closeHistory()">

                ✕ Κλείσιμο

            </button>

        </div>

        <div
            id="history"
            class="history">
        </div>

    </div>


    <div class="model-info">

        The Weather Company (TWC) Forecast system

        <br>

        Ιστορικό: ECMWF ERA5 Reanalysis
        μέσω Open-Meteo — διαθέσιμο από το 1940.

        <br>

        Τα δεδομένα ανανεώνονται αυτόματα
        σύμφωνα με τους κύκλους έκδοσης
        του παρόχου.

    </div>


</div>



<script>

/* =========================================================
   THE WEATHER COMPANY (TWC)
   =========================================================

   ΒΑΛΕ ΕΔΩ ΤΟ ΔΙΚΟ ΣΟΥ TWC API KEY
*/

const TWC_API_KEY = "ΒΑΛΕ_ΕΔΩ_ΤΟ_TWC_API_KEY";


const TWC_BASE =
    "https://api.weather.com";


const TWC_LANGUAGE =
    "el-GR";


let weatherData = null;

let locationData = null;

let historyYears = 1;


/* =====================================
   MENU
===================================== */

function toggleMenu(){

    const menu =
        document.getElementById("menu");

    menu.classList.toggle("open");

}


function closeMenu(){

    document
        .getElementById("menu")
        .classList.remove("open");

}


function refreshWeather(){

    closeMenu();

    closeHistory();

    if(locationData){

        loadWeather();

    }else{

        searchCity();

    }

}


function goTop(){

    window.scrollTo({

        top:0,

        behavior:"smooth"

    });

}


/* =====================================
   HISTORY
===================================== */

function openHistorySelector(){

    closeMenu();

    closeHourly();

    if(!locationData){

        alert(
            "Πρώτα αναζήτησε μία τοποθεσία."
        );

        return;

    }


    const historySection =
        document.getElementById(
            "historySection"
        );


    historySection.style.display =
        "block";


    renderHistoryRangeSelector();


    historySection.scrollIntoView({

        behavior:"smooth",

        block:"start"

    });

}


function renderHistoryRangeSelector(){

    const history =
        document.getElementById(
            "history"
        );


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="closeHistory()">

                ✕ Κλείσιμο

            </button>

        </div>

        <div class="history-range-title">

            Επίλεξε πόσα τελευταία έτη
            θέλεις να εμφανιστούν

        </div>

        <div class="history-ranges">

    `;


    for(
        let years = 1;
        years <= 10;
        years++
    ){

        html += `

            <button
                class="history-range-button"
                onclick="loadHistory(${years})">

                ${years}
                ${years === 1 ? "έτος" : "έτη"}

            </button>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +
        locationData.name;

}


function loadHistory(years){

    if(!locationData){

        alert(
            "Πρώτα αναζήτησε μία τοποθεσία."
        );

        return;

    }


    historyYears = years;


    const historySection =
        document.getElementById(
            "historySection"
        );


    historySection.style.display =
        "block";


    renderHistoryYears(years);


    historySection.scrollIntoView({

        behavior:"smooth",

        block:"start"

    });

}


function renderHistoryYears(years){

    const history =
        document.getElementById(
            "history"
        );


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="renderHistoryRangeSelector()">

                ← 1–10 έτη

            </button>

        </div>

        <div class="history-years">

    `;


    const currentYear =
        new Date().getFullYear();


    for(
        let i = 0;
        i < years;
        i++
    ){

        const year =
            currentYear - i;


        html += `

            <button
                class="history-year-button"
                onclick="loadHistoryMonths(${year})">

                📅 ${year}

            </button>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +
        locationData.name +
        " — επίλεξε έτος";

}


function loadHistoryMonths(year){

    const history =
        document.getElementById(
            "history"
        );


    const months = [

        "Ιανουάριος",
        "Φεβρουάριος",
        "Μάρτιος",
        "Απρίλιος",
        "Μάιος",
        "Ιούνιος",
        "Ιούλιος",
        "Αύγουστος",
        "Σεπτέμβριος",
        "Οκτώβριος",
        "Νοέμβριος",
        "Δεκέμβριος"

    ];


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="renderHistoryYears(historyYears)">

                ← Έτη

            </button>

        </div>

        <div class="history-months">

    `;


    for(
        let month = 1;
        month <= 12;
        month++
    ){

        html += `

            <button
                class="history-month-button"
                onclick="loadHistoryMonth(${year},${month})">

                📅 ${months[month - 1]}

            </button>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +
        locationData.name +
        " — " +
        year;

}


async function loadHistoryMonth(
    year,
    month
){

    if(!locationData){

        return;

    }


    const history =
        document.getElementById(
            "history"
        );


    history.innerHTML = `

        <div class="loading">

            Φόρτωση ιστορικού
            ${month}/${year}...

        </div>

    `;


    const monthNames = [

        "Ιανουάριος",
        "Φεβρουάριος",
        "Μάρτιος",
        "Απρίλιος",
        "Μάιος",
        "Ιούνιος",
        "Ιούλιος",
        "Αύγουστος",
        "Σεπτέμβριος",
        "Οκτώβριος",
        "Νοέμβριος",
        "Δεκέμβριος"

    ];


    try{

        const startDate =
            `${year}-${String(month).padStart(2,"0")}-01`;


        const lastDay =
            new Date(
                Date.UTC(
                    year,
                    month,
                    0
                )
            ).getUTCDate();


        const endDate =
            `${year}-${String(month).padStart(2,"0")}-${String(lastDay).padStart(2,"0")}`;


        const url =

            "https://archive-api.open-meteo.com/v1/archive" +

            "?latitude=" +
            encodeURIComponent(locationData.latitude) +

            "&longitude=" +
            encodeURIComponent(locationData.longitude) +

            "&start_date=" +
            startDate +

            "&end_date=" +
            endDate +

            "&daily=" +
            "weather_code," +
            "temperature_2m_max," +
            "temperature_2m_min" +

            "&models=era5" +

            "&timezone=auto";


        const response =
            await fetch(url);


        if(!response.ok){

            throw new Error(
                "History request failed"
            );

        }


        const data =
            await response.json();


        if(
            !data.daily ||
            !data.daily.time ||
            !data.daily.time.length
        ){

            throw new Error(
                "No history data"
            );

        }


        renderHistoryMonth(
            data,
            year,
            month,
            monthNames[month - 1]
        );


    }catch(error){

        console.error(error);


        history.innerHTML = `

            <div class="loading">

                Δεν ήταν δυνατή η φόρτωση
                του ιστορικού.

                <br><br>

                <button
                    class="history-back-button"
                    onclick="loadHistoryMonths(${year})">

                    ← Επιστροφή στους μήνες

                </button>

            </div>

        `;

    }

}


function renderHistoryMonth(
    data,
    year,
    month,
    monthName
){

    const d =
        data.daily;


    const history =
        document.getElementById(
            "history"
        );


    let html = `

        <div class="history-navigation">

            <button
                class="history-back-button"
                onclick="loadHistoryMonths(${year})">

                ← ${year}

            </button>

        </div>

        <div class="history-days">

    `;


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){

        const rawDate =
            d.time[i];


        const dateParts =
            rawDate.split("-");


        const dayNumber =
            Number(dateParts[2]);


        const monthNumber =
            Number(dateParts[1]);


        const yearNumber =
            Number(dateParts[0]);


        const date =
            `${dayNumber}/${monthNumber}/${yearNumber}`;


        const max =
            Math.round(
                Number(
                    d.temperature_2m_max[i]
                )
            );


        const min =
            Math.round(
                Number(
                    d.temperature_2m_min[i]
                )
            );


        html += `

            <div
                class="history-day"
                title="${date}"
            >

                <div class="history-date">

                    ${date}

                </div>


                <div class="history-day-content">


                    <div
                        class="history-thermometer"
                        aria-label="Θερμοκρασία">

                        <div
                            class="history-thermometer-fill">
                        </div>

                        <div
                            class="history-thermometer-bulb">
                        </div>

                    </div>


                    <div class="history-temperature">

                        <div class="day-temp">

                            ${max}°

                        </div>

                        <div class="night-temp">

                            ${min}°

                        </div>

                    </div>


                </div>

            </div>

        `;

    }


    html += `

        </div>

    `;


    history.innerHTML =
        html;


    document
        .getElementById("historyTitle")
        .innerText =

        "📜 Ιστορικό καιρού — " +

        locationData.name +

        " — " +

        monthName +

        " " +

        year;

}


function closeHistory(){

    const section =
        document.getElementById(
            "historySection"
        );


    if(section){

        section.style.display =
            "none";

    }

}


/* =====================================
   MENU CLICK OUTSIDE
===================================== */

document.addEventListener(
    "click",
    function(event){

        const menu =
            document.getElementById("menu");

        const button =
            document.querySelector(".menu-button");


        if(
            menu.classList.contains("open") &&
            !menu.contains(event.target) &&
            !button.contains(event.target)
        ){

            menu.classList.remove("open");

        }

    }
);


/* =====================================
   HELPERS
===================================== */

function countryFlag(countryCode){

    if(!countryCode){

        return "🌍";

    }


    const code =
        countryCode
        .toUpperCase()
        .trim();


    if(code.length !== 2){

        return "🌍";

    }


    return String
        .fromCodePoint(
            ...[...code].map(
                char =>
                    127397 +
                    char.charCodeAt(0)
            )
        );

}


function windDirection(degrees){

    if(
        degrees === null ||
        degrees === undefined ||
        isNaN(degrees)
    ){

        return "—";

    }


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
        Math.round(
            degrees / 22.5
        ) % 16;


    return directions[index];

}


const greekDays = [

    "Κυρ",
    "Δευ",
    "Τρί",
    "Τετ",
    "Πέμ",
    "Παρ",
    "Σάβ"

];


function formatDate(
    dateString,
    includeYear = false
){

    const parts =
        dateString.split("-");


    const year =
        Number(parts[0]);


    const month =
        Number(parts[1]);


    const day =
        Number(parts[2]);


    const d =
        new Date(
            Date.UTC(
                year,
                month - 1,
                day
            )
        );


    let formattedDate =

        String(day) +
        "/" +
        String(month);


    if(includeYear){

        formattedDate +=

            "/" +
            String(year);

    }


    return {

        day:
            greekDays[d.getUTCDay()],

        date:
            formattedDate

    };

}


/* =====================================
   TWC WEATHER ICONS
===================================== */

function twcWeatherIcon(
    iconCode,
    isDay = true
){

    const code =
        Number(iconCode);


    /*
       TWC icon codes:
       1-4  sunny / mostly sunny / partly cloudy / intermittent clouds
       5-12 precipitation/fog
       13-18 snow/mix
       19-25 fog/wind
       26-30 clouds/partly cloudy
       31-34 clear/mostly clear/partly cloudy
       35-47 mixed precipitation/thunder
    */


    if(
        [1,2].includes(code)
    ){

        return isDay
            ? "☀️"
            : '<span class="night-moon">🌙</span>';

    }


    if(
        [3,4].includes(code)
    ){

        return isDay
            ? "🌤️"
            : `
                <span
                    class="night-partly-cloudy"
                    aria-label="Λίγες νεφώσεις τη νύχτα">
                </span>
            `;

    }


    if(
        [31,33].includes(code)
    ){

        return '<span class="night-moon">🌙</span>';

    }


    if(
        [32,34].includes(code)
    ){

        return isDay
            ? "🌤️"
            : `
                <span
                    class="night-partly-cloudy"
                    aria-label="Λίγες νεφώσεις τη νύχτα">
                </span>
            `;

    }


    if(
        [26,27,28,29,30].includes(code)
    ){

        return "☁️";

    }


    if(
        [11,20,21,22,23,24].includes(code)
    ){

        return "🌫️";

    }


    if(
        [5,6,7,8,9,10,12,39,40].includes(code)
    ){

        return "🌧️";

    }


    if(
        [13,14,15,16,17,18,41,42,43,44].includes(code)
    ){

        return "🌨️";

    }


    if(
        [25,35].includes(code)
    ){

        return "🌨️";

    }


    if(
        [37,38,47].includes(code)
    ){

        return "⛈️";

    }


    return "☁️";

}


/* =====================================
   TWC WEATHER TEXT
===================================== */

function translateTWCText(text){

    if(!text){

        return "Μεταβλητός καιρός";

    }


    const t =
        String(text)
        .toLowerCase();


    if(
        t.includes("thunderstorm") ||
        t.includes("thunder")
    ){

        return "Καταιγίδα";

    }


    if(
        t.includes("snow") &&
        (
            t.includes("rain") ||
            t.includes("mix") ||
            t.includes("sleet")
        )
    ){

        return "Χιονόνερο";

    }


    if(t.includes("snow")){

        return "Χιόνι";

    }


    if(
        t.includes("freezing rain") ||
        t.includes("sleet")
    ){

        return "Χιονόνερο";

    }


    if(
        t.includes("drizzle") ||
        t.includes("light rain")
    ){

        return "Ψιλόβροχο";

    }


    if(
        t.includes("rain") ||
        t.includes("shower")
    ){

        return "Βροχή";

    }


    if(
        t.includes("fog") ||
        t.includes("haze")
    ){

        return "Ομίχλη";

    }


    if(
        t.includes("mostly sunny") ||
        t.includes("mostly clear")
    ){

        return "Κυρίως αίθριος";

    }


    if(
        t.includes("partly cloudy") ||
        t.includes("partly sunny")
    ){

        return "Λίγες νεφώσεις";

    }


    if(
        t.includes("mostly cloudy")
    ){

        return "Κυρίως συννεφιά";

    }


    if(
        t.includes("cloudy") ||
        t.includes("overcast")
    ){

        return "Συννεφιά";

    }


    if(
        t.includes("clear") ||
        t.includes("sunny")
    ){

        return "Αίθριος";

    }


    return text;

}


/* =====================================
   TWC API HELPER
===================================== */

async function twcFetch(
    endpoint,
    params = {}
){

    if(
        !TWC_API_KEY ||
        TWC_API_KEY === "ΒΑΛΕ_ΕΔΩ_ΤΟ_TWC_API_KEY"
    ){

        throw new Error(
            "Δεν έχει τοποθετηθεί TWC API key."
        );

    }


    const url =
        new URL(
            TWC_BASE + endpoint
        );


    Object.entries(params).forEach(
        ([key,value]) => {

            if(
                value !== undefined &&
                value !== null
            ){

                url.searchParams.set(
                    key,
                    value
                );

            }

        }
    );


    url.searchParams.set(
        "apiKey",
        TWC_API_KEY
    );


    const response =
        await fetch(
            url.toString()
        );


    if(!response.ok){

        let message =
            "TWC request failed: " +
            response.status;


        try{

            const errorData =
                await response.json();

            if(errorData.message){

                message +=
                    " — " +
                    errorData.message;

            }

        }catch(e){}


        throw new Error(message);

    }


    return response.json();

}


/* =====================================
   SEARCH CITY — TWC LOCATION MASTER
===================================== */

async function searchCity(){

    const city =
        document
        .getElementById("cityInput")
        .value
        .trim();


    if(!city)
        return;


    closeHistory();

    closeHourly();


    document
        .getElementById("forecast")
        .innerHTML =

        `<div class="loading">

            Αναζήτηση πόλης...

         </div>`;


    try{

        const geo =
            await twcFetch(
                "/v3/location/search",
                {

                    query:
                        city,

                    language:
                        TWC_LANGUAGE,

                    format:
                        "json",

                    locationType:
                        "city,locality,address"

                }
            );


        if(
            !geo.location ||
            !geo.location.latitude ||
            !geo.location.latitude.length
        ){

            throw new Error(
                "Δεν βρέθηκε η πόλη."
            );

        }


        const place =
            geo.location;


        locationData = {

            name:
                place.displayName?.[0] ||
                place.city?.[0] ||
                city,

            latitude:
                place.latitude[0],

            longitude:
                place.longitude[0],

            country:
                place.country?.[0] ||
                "",

            countryCode:
                place.countryCode?.[0] ||
                "",

            placeId:
                place.placeId?.[0] ||
                null

        };


        await loadWeather();


    }catch(error){

        console.error(error);


        document
            .getElementById("forecast")
            .innerHTML =

            `<div class="loading">

                Σφάλμα φόρτωσης δεδομένων.

                <br><br>

                ${error.message || ""}

             </div>`;

    }

}


/* =====================================
   LOAD WEATHER FROM TWC
===================================== */

async function loadWeather(){

    if(!locationData){

        return;

    }


    document
        .getElementById("current")
        .innerHTML =

        `<div class="current">

            <div class="loading">

                Φόρτωση καιρού...

            </div>

        </div>`;


    document
        .getElementById("forecast")
        .innerHTML =

        `<div class="loading">

            Φόρτωση πρόγνωσης...

        </div>`;


    const geocode =
        locationData.latitude +
        "," +
        locationData.longitude;


    try{

        const [

            currentData,
            dailyData,
            hourlyData

        ] = await Promise.all([

            twcFetch(
                "/v3/wx/observations/current",
                {

                    geocode:
                        geocode,

                    units:
                        "m",

                    language:
                        TWC_LANGUAGE,

                    format:
                        "json"

                }
            ),

            twcFetch(
                "/v3/wx/forecast/daily/15day",
                {

                    geocode:
                        geocode,

                    units:
                        "m",

                    language:
                        TWC_LANGUAGE,

                    format:
                        "json"

                }
            ),

            twcFetch(
                "/v3/wx/forecast/hourly/15day",
                {

                    geocode:
                        geocode,

                    units:
                        "m",

                    language:
                        TWC_LANGUAGE,

                    format:
                        "json"

                }
            )

        ]);


        weatherData = {

            current:
                Array.isArray(currentData)
                    ? currentData[0]
                    : currentData,

            daily:
                dailyData,

            hourly:
                hourlyData

        };


        renderCurrent();

        renderForecast();


    }catch(error){

        console.error(error);


        document
            .getElementById("current")
            .innerHTML = "";


        document
            .getElementById("forecast")
            .innerHTML =

            `<div class="loading">

                Δεν ήταν δυνατή η φόρτωση
                των δεδομένων TWC.

                <br><br>

                ${error.message || ""}

             </div>`;

    }

}


/* =====================================
   CURRENT
===================================== */

function renderCurrent(){

    const d =
        weatherData.current;


    const temp =
        Number(
            d.temperature
        );


    const humidity =
        Number(
            d.relativeHumidity
        );


    const wind =
        Number(
            d.windSpeed
        );


    const windDir =
        d.windDirectionCardinal ||
        windDirection(
            d.windDirection
        );


    const feels =
        Number(
            d.temperatureFeelsLike
        );


    const code =
        Number(
            d.iconCode
        );


    const isDay =
        d.dayOrNight !== "N";


    document
        .getElementById("current")
        .innerHTML = `

        <div class="current">

            <h2>

                ${locationData.name}

                <div style="
                    font-size:16px;
                    font-weight:normal;
                    color:#dce5ee;
                    margin-top:7px;
                ">

                    ${countryFlag(
                        locationData.countryCode
                    )}

                    ${locationData.country}

                </div>

            </h2>


            <div class="temperature">

                ${Math.round(temp)}°C

            </div>


            <div class="condition">

                ${twcWeatherIcon(
                    code,
                    isDay
                )}

                ${translateTWCText(
                    d.wxPhraseLong
                )}

            </div>


            <div class="current-grid">


                <div class="current-box">

                    <span>
                        💧 Υγρασία
                    </span>

                    <strong>

                        ${Math.round(humidity)}%

                    </strong>

                </div>


                <div class="current-box">

                    <span>
                        🌬️ Άνεμος
                    </span>

                    <strong>

                        ${Math.round(wind)}
                        km/h
                        —
                        ${windDir}

                    </strong>

                </div>


                <div class="current-box">

                    <span>
                        🌡️ Αίσθηση
                    </span>

                    <strong>

                        ${Math.round(feels)}°C

                    </strong>

                </div>


            </div>

        </div>

    `;

}


/* =====================================
   FORECAST 15 DAYS
===================================== */

function renderForecast(){

    const d =
        weatherData.daily;


    const times =
        d.validTimeLocal || [];


    const maxTemps =
        d.temperatureMax || [];


    const minTemps =
        d.temperatureMin || [];


    const rainProb =
        d.daypart &&
        d.daypart[0] &&
        d.daypart[0].precipChance
            ? d.daypart[0].precipChance
            : [];


    const icons =
        d.daypart &&
        d.daypart[0] &&
        d.daypart[0].iconCode
            ? d.daypart[0].iconCode
            : [];


    const phrases =
        d.daypart &&
        d.daypart[0] &&
        d.daypart[0].wxPhraseLong
            ? d.daypart[0].wxPhraseLong
            : [];


    let html = "";


    for(
        let i = 0;
        i < Math.min(15,times.length);
        i++
    ){

        const localDate =
            times[i].substring(
                0,
                10
            );


        const date =
            formatDate(
                localDate
            );


        const max =
            Number(
                maxTemps[i]
            );


        const min =
            Number(
                minTemps[i]
            );


        const rain =
            Number(
                rainProb[i] || 0
            );


        const iconCode =
            Number(
                icons[i]
                || 30
            );


        const precipitationInfo =

            `💧 ${Math.round(rain)}%`;


        html += `

        <div
            class="day"
            onclick="showHourly(${i})"
        >

            <div class="day-name">

                ${date.day}

            </div>


            <div class="date">

                ${date.date}

            </div>


            <div class="icon">

                ${twcWeatherIcon(
                    iconCode,
                    true
                )}

            </div>


            <div class="max">

                ${Math.round(max)}°

            </div>


            <div class="min">

                ${Math.round(min)}°

            </div>


            <div class="rain">

                ${precipitationInfo}

            </div>


        </div>

        `;

    }


    document
        .getElementById("forecast")
        .innerHTML =
        html;

}


/* =====================================
   HOURLY TWC
===================================== */

function showHourly(dayIndex){

    const d =
        weatherData.hourly;


    const daily =
        weatherData.daily;


    const dailyTime =
        daily.validTimeLocal[
            dayIndex
        ];


    const date =
        dailyTime.substring(
            0,
            10
        );


    const times =
        d.validTimeLocal || [];


    const rows = [];


    for(
        let i = 0;
        i < times.length;
        i++
    ){

        if(
            times[i].substring(
                0,
                10
            ) === date
        ){

            rows.push(i);

        }

    }


    const formatted =
        formatDate(date);


    document
        .getElementById("hourlyTitle")
        .innerText =

        "Πρόγνωση ανά ώρα — " +

        formatted.day +

        " " +

        formatted.date;


    let html = "";


    rows.forEach(i => {

        const fullTime =
            times[i];


        const timeMatch =
            fullTime.match(
                /T(\d{2}:\d{2})/
            );


        const hour =
            timeMatch
                ? timeMatch[1]
                : fullTime.substring(
                    11,
                    16
                );


        const temp =
            Math.round(
                Number(
                    d.temperature?.[i]
                )
            );


        const feels =
            Math.round(
                Number(
                    d.temperatureFeelsLike?.[i]
                )
            );


        const rain =
            Math.round(
                Number(
                    d.precipChance?.[i]
                    || 0
                )
            );


        const wind =
            Math.round(
                Number(
                    d.windSpeed?.[i]
                    || 0
                )
            );


        const windDir =
            d.windDirectionCardinal?.[i]
            ||
            windDirection(
                d.windDirection?.[i]
            );


        const clouds =
            Math.round(
                Number(
                    d.cloudCover?.[i]
                    || 0
                )
            );


        const iconCode =
            Number(
                d.iconCode?.[i]
                || 30
            );


        const dayOrNight =
            d.dayOrNight?.[i]
            || "D";


        const isDay =
            dayOrNight !== "N";


        const icon =
            twcWeatherIcon(
                iconCode,
                isDay
            );


        let precipitationHTML = `

            💧 ${rain}%

        `;


        const precipType =
            d.precipType?.[i];


        if(
            precipType &&
            String(precipType)
            .toLowerCase()
            .includes("snow")
        ){

            precipitationHTML = `

                ❄️ ${rain}%

            `;

        }


        html += `

        <div class="hour">


            <div class="hour-time">

                ${hour}

            </div>


            <div class="hour-icon">

                ${icon}

            </div>


            <div class="hour-data">

                🌡️

                <b>
                    ${temp}°
                </b>

                <br>

                Αίσθηση
                ${feels}°

            </div>


            <div class="hour-data">

                ${precipitationHTML}

            </div>


            <div class="hour-data">

                ☁️
                ${clouds}%

            </div>


            <div class="hour-data">

                🌬️
                ${wind} km/h

                <br>

                Διεύθυνση:
                <b>
                    ${windDir}
                </b>

            </div>


        </div>

        `;

    });


    if(!html){

        html = `

            <div class="loading">

                Δεν υπάρχουν διαθέσιμα
                ωριαία δεδομένα για αυτή την ημέρα.

            </div>

        `;

    }


    document
        .getElementById("hourly")
        .innerHTML =
        html;


    const section =
        document
        .getElementById(
            "hourlySection"
        );


    section.style.display =
        "block";


    section.scrollIntoView({

        behavior:"smooth",

        block:"start"

    });

}


function closeHourly(){

    document
        .getElementById(
            "hourlySection"
        )
        .style.display =
        "none";

}


/* =====================================
   ENTER SEARCH
===================================== */

document
    .getElementById("cityInput")
    .addEventListener(
        "keydown",
        function(e){

            if(e.key === "Enter"){

                searchCity();

            }

        }
    );


/* =====================================
   START
===================================== */

searchCity();


</script>


</body>

</html>

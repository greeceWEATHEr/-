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
   ΩΡΙΑΙΑ
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

.history-days{
    display:grid;
    grid-template-columns:
        repeat(6,minmax(0,1fr));
    gap:10px;
}

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

.history-day-content{
    display:flex;
    align-items:center;
    justify-content:center;
    gap:10px;
    width:100%;
    flex:1;
}

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
}

.history-temperature .night-temp{
    color:#d0d7df;
}

.history-thermometer{
    position:relative;
    width:18px;
    height:54px;
    flex:0 0 18px;
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

.model-info{
    margin-top:18px;
    color:#bdc9d6;
    font-size:12px;
    line-height:1.5;
}

.loading{
    text-align:center;
    padding:30px;
    font-size:16px;
}


/* =====================================
   MOBILE
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
        value="Θεσσαλονίκη">

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

    ECMWF IFS HRES • ECMWF AIFS • NOAA GFS • DWD ICON

    <br>

    Ιστορικό: ECMWF ERA5 Reanalysis
    μέσω Open-Meteo — διαθέσιμο από το 1940.

    <br>

    Τα δεδομένα ανανεώνονται αυτόματα
    σύμφωνα με τους κύκλους έκδοσης
    των μοντέλων.

</div>


</div>


<script>


/* =========================================================
   GLOBAL
========================================================= */

let weatherData = null;

let locationData = null;

let historyYears = 1;

let refreshTimer = null;

let loadingRequest = false;


/* =========================================================
   MODEL WEIGHTS
========================================================= */

/*
   Δεν είναι επίσημα βάρη TWC.

   Είναι multi-model blend για να μην εξαρτάται
   η ιστοσελίδα από ένα μόνο numerical model.
*/

const MODEL_WEIGHTS = {

    ecmwf:0.40,

    aifs:0.25,

    gfs:0.20,

    icon:0.15

};


/* =========================================================
   MENU
========================================================= */

function toggleMenu(){

    document
        .getElementById("menu")
        .classList.toggle("open");

}


function closeMenu(){

    document
        .getElementById("menu")
        .classList.remove("open");

}


/* =========================================================
   HISTORY MENU
========================================================= */

function openHistorySelector(){

    closeMenu();

    closeHourly();

    if(!locationData){

        alert(
            "Πρώτα αναζήτησε μία τοποθεσία."
        );

        return;

    }

    const section =
        document.getElementById(
            "historySection"
        );

    section.style.display =
        "block";

    renderHistoryRangeSelector();

    section.scrollIntoView({

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
        let years=1;
        years<=10;
        years++
    ){

        html += `

            <button
                class="history-range-button"
                onclick="loadHistory(${years})">

                ${years}
                ${years===1 ? "έτος":"έτη"}

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

    historyYears =
        years;

    renderHistoryYears(years);

}


function renderHistoryYears(years){

    const history =
        document.getElementById(
            "history"
        );

    const currentYear =
        new Date().getFullYear();

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


    for(
        let i=0;
        i<years;
        i++
    ){

        const year =
            currentYear-i;

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
        let month=1;
        month<=12;
        month++
    ){

        html += `

            <button
                class="history-month-button"
                onclick="loadHistoryMonth(${year},${month})">

                📅 ${months[month-1]}

            </button>

        `;

    }


    html += `

        </div>

    `;


    document
        .getElementById("history")
        .innerHTML =
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

            "&daily=weather_code,temperature_2m_max,temperature_2m_min" +

            "&models=era5" +

            "&timezone=auto";


        const response =
            await fetch(
                url,
                {
                    cache:"no-store"
                }
            );


        if(!response.ok){

            throw new Error(
                "History request failed"
            );

        }


        const data =
            await response.json();


        renderHistoryMonth(
            data,
            year,
            month,
            monthNames[month-1]
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

                    ← Επιστροφή

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
        let i=0;
        i<d.time.length;
        i++
    ){

        const parts =
            d.time[i].split("-");

        const date =
            `${Number(parts[2])}/${Number(parts[1])}/${Number(parts[0])}`;

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

            <div class="history-day">

                <div class="history-date">

                    ${date}

                </div>

                <div class="history-day-content">

                    <div
                        class="history-thermometer">

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


    document
        .getElementById("history")
        .innerHTML =
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

    document
        .getElementById(
            "historySection"
        )
        .style.display =
        "none";

}


/* =========================================================
   COUNTRY FLAG
========================================================= */

function countryFlag(countryCode){

    if(!countryCode){

        return "🌍";

    }

    const code =
        countryCode
        .toUpperCase()
        .trim();


    if(code.length!==2){

        return "🌍";

    }


    return String.fromCodePoint(
        ...[...code].map(
            char =>
                127397 +
                char.charCodeAt(0)
        )
    );

}


/* =========================================================
   WEATHER ICON
   ΚΡΑΤΑΜΕ ΤΗ ΔΙΚΗ ΣΟΥ ΛΟΓΙΚΗ
========================================================= */

function weatherIcon(
    code,
    isDay=true,
    precipitationProbability=0,
    snowfall=0
){

    const rain =
        Number(
            precipitationProbability||0
        );

    const snow =
        Number(
            snowfall||0
        );


    if(rain<30){

        if(code===0){

            if(isDay)
                return "☀️";

            return '<span class="night-moon">🌙</span>';

        }


        if(code===1){

            if(isDay)
                return "🌤️";

            return '<span class="night-moon">🌙</span>';

        }


        if(code===2){

            if(isDay)
                return "🌤️";

            return `
                <span
                    class="night-partly-cloudy"
                    aria-label="Λίγες νεφώσεις τη νύχτα">
                </span>
            `;

        }


        if(code===3)
            return "☁️";


        if([45,48].includes(code))
            return "🌫️";


        if([
            51,53,55,56,57,
            61,63,65,66,67,
            71,73,75,77,
            80,81,82,
            85,86,
            95,96,99
        ].includes(code))
            return "☁️";


        if(isDay)
            return "🌤️";

        return '<span class="night-moon">🌙</span>';

    }


    if([95,96,99].includes(code))
        return "⛈️";


    if(
        snow>0 ||
        [71,73,75,77,85,86].includes(code)
    )
        return "🌨️";


    if([
        51,53,55,56,57,
        61,63,65,66,67,
        80,81,82
    ].includes(code))
        return "🌧️";


    return "🌧️";

}


/* =========================================================
   WEATHER TEXT
========================================================= */

function weatherText(code){

    if(code===0)
        return "Αίθριος";

    if(code===1)
        return "Κυρίως αίθριος";

    if(code===2)
        return "Λίγες νεφώσεις";

    if(code===3)
        return "Συννεφιά";

    if([45,48].includes(code))
        return "Ομίχλη";

    if([51,53,55,56,57].includes(code))
        return "Ψιλόβροχο";

    if([61,63,65].includes(code))
        return "Βροχή";

    if([66,67].includes(code))
        return "Χιονόνερο";

    if([71,73,75,77].includes(code))
        return "Χιόνι";

    if([80,81,82].includes(code))
        return "Μπόρες";

    if([85,86].includes(code))
        return "Χιονομπόρες";

    if([95,96,99].includes(code))
        return "Καταιγίδα";

    return "Μεταβλητός καιρός";

}


/* =========================================================
   WIND DIRECTION
========================================================= */

function windDirection(degrees){

    if(
        degrees===null ||
        degrees===undefined ||
        isNaN(degrees)
    )
        return "—";


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


    return directions[
        Math.round(
            degrees/22.5
        )%16
    ];

}


/* =========================================================
   WEIGHTED AVERAGE
========================================================= */

function weightedAverage(values){

    let total=0;

    let totalWeight=0;


    values.forEach(item=>{

        const value =
            Number(item.value);

        const weight =
            Number(item.weight);


        if(
            Number.isFinite(value) &&
            Number.isFinite(weight) &&
            weight>0
        ){

            total +=
                value*weight;

            totalWeight +=
                weight;

        }

    });


    if(!totalWeight)
        return null;


    return total/totalWeight;

}


/* =========================================================
   WIND CIRCULAR AVERAGE
========================================================= */

function weightedWindDirection(items){

    let sinTotal=0;

    let cosTotal=0;

    let totalWeight=0;


    items.forEach(item=>{

        const value =
            Number(item.value);

        const weight =
            Number(item.weight);


        if(
            !Number.isFinite(value) ||
            !Number.isFinite(weight)
        )
            return;


        const rad =
            value*Math.PI/180;


        sinTotal +=
            Math.sin(rad)*weight;

        cosTotal +=
            Math.cos(rad)*weight;

        totalWeight +=
            weight;

    });


    if(!totalWeight)
        return null;


    let degrees =
        Math.atan2(
            sinTotal,
            cosTotal
        )*180/Math.PI;


    if(degrees<0)
        degrees+=360;


    return degrees;

}


/* =========================================================
   WEATHER CODE COMBINATION
========================================================= */

function combinedWeatherCode(items){

    const scores={};


    items.forEach(item=>{

        const code =
            Number(item.value);

        const weight =
            Number(item.weight);


        if(
            !Number.isFinite(code) ||
            !Number.isFinite(weight)
        )
            return;


        scores[code] =
            (scores[code]||0)+weight;

    });


    let bestCode=0;

    let bestScore=-1;


    Object.keys(scores).forEach(code=>{

        if(scores[code]>bestScore){

            bestScore =
                scores[code];

            bestCode =
                Number(code);

        }

    });


    return bestCode;

}


/* =========================================================
   MODELS AVAILABLE
========================================================= */

function availableModels(){

    const list=[];


    if(weatherData?.ecmwf)
        list.push("ecmwf");

    if(weatherData?.aifs)
        list.push("aifs");

    if(weatherData?.gfs)
        list.push("gfs");

    if(weatherData?.icon)
        list.push("icon");


    return list;

}


/* =========================================================
   BLENDED CURRENT
========================================================= */

function getBlendedCurrent(){

    const models =
        availableModels();


    if(!models.length)
        return null;


    const temperature=[];
    const humidity=[];
    const apparent=[];
    const wind=[];
    const direction=[];
    const codes=[];


    models.forEach(name=>{

        const d =
            weatherData[name];


        if(!d?.current)
            return;


        const weight =
            MODEL_WEIGHTS[name];


        temperature.push({

            value:d.current.temperature_2m,
            weight

        });


        humidity.push({

            value:d.current.relative_humidity_2m,
            weight

        });


        apparent.push({

            value:d.current.apparent_temperature,
            weight

        });


        wind.push({

            value:d.current.wind_speed_10m,
            weight

        });


        direction.push({

            value:d.current.wind_direction_10m,
            weight

        });


        codes.push({

            value:d.current.weather_code,
            weight

        });

    });


    return {

        temperature:
            weightedAverage(temperature),

        humidity:
            weightedAverage(humidity),

        apparent:
            weightedAverage(apparent),

        wind:
            weightedAverage(wind),

        windDirection:
            weightedWindDirection(direction),

        weatherCode:
            combinedWeatherCode(codes),

        isDay:
            weatherData.ecmwf?.current?.is_day===1

    };

}


/* =========================================================
   BLENDED DAILY
========================================================= */

function getBlendedDaily(){

    const base =
        weatherData.ecmwf.daily;


    const result={

        time:
            base.time.slice(),

        temperature_2m_max:[],
        temperature_2m_min:[],
        weather_code:[],
        precipitation_probability_max:[],
        snowfall_sum:[],
        precipitation_sum:[],
        wind_speed_10m_max:[],
        sunrise:base.sunrise,
        sunset:base.sunset

    };


    for(
        let day=0;
        day<base.time.length;
        day++
    ){

        const max=[];
        const min=[];
        const prob=[];
        const snow=[];
        const precip=[];
        const wind=[];
        const codes=[];


        availableModels().forEach(name=>{

            const d =
                weatherData[name].daily;


            if(
                !d ||
                day>=d.time.length
            )
                return;


            const weight =
                MODEL_WEIGHTS[name];


            max.push({

                value:
                    d.temperature_2m_max[day],

                weight

            });


            min.push({

                value:
                    d.temperature_2m_min[day],

                weight

            });


            prob.push({

                value:
                    d.precipitation_probability_max[day],

                weight

            });


            snow.push({

                value:
                    d.snowfall_sum[day],

                weight

            });


            precip.push({

                value:
                    d.precipitation_sum[day],

                weight

            });


            wind.push({

                value:
                    d.wind_speed_10m_max[day],

                weight

            });


            codes.push({

                value:
                    d.weather_code[day],

                weight

            });

        });


        result.temperature_2m_max.push(
            weightedAverage(max)
        );

        result.temperature_2m_min.push(
            weightedAverage(min)
        );

        result.precipitation_probability_max.push(
            weightedAverage(prob)
        );

        result.snowfall_sum.push(
            weightedAverage(snow)
        );

        result.precipitation_sum.push(
            weightedAverage(precip)
        );

        result.wind_speed_10m_max.push(
            weightedAverage(wind)
        );

        result.weather_code.push(
            combinedWeatherCode(codes)
        );

    }


    return result;

}


/* =========================================================
   BLENDED HOURLY
========================================================= */

function getBlendedHourly(){

    const base =
        weatherData.ecmwf.hourly;


    const result={

        time:
            base.time.slice(),

        temperature_2m:[],
        relative_humidity_2m:[],
        apparent_temperature:[],
        precipitation:[],
        precipitation_probability:[],
        snowfall:[],
        weather_code:[],
        cloud_cover:[],
        wind_speed_10m:[],
        wind_direction_10m:[],
        is_day:
            base.is_day.slice()

    };


    for(
        let hour=0;
        hour<base.time.length;
        hour++
    ){

        const temperature=[];
        const humidity=[];
        const apparent=[];
        const precipitation=[];
        const probability=[];
        const snowfall=[];
        const clouds=[];
        const wind=[];
        const direction=[];
        const codes=[];


        availableModels().forEach(name=>{

            const d =
                weatherData[name].hourly;


            if(
                !d ||
                hour>=d.time.length
            )
                return;


            const weight =
                MODEL_WEIGHTS[name];


            temperature.push({

                value:d.temperature_2m[hour],
                weight

            });


            humidity.push({

                value:d.relative_humidity_2m[hour],
                weight

            });


            apparent.push({

                value:d.apparent_temperature[hour],
                weight

            });


            precipitation.push({

                value:d.precipitation[hour],
                weight

            });


            probability.push({

                value:d.precipitation_probability[hour],
                weight

            });


            snowfall.push({

                value:d.snowfall[hour],
                weight

            });


            clouds.push({

                value:d.cloud_cover[hour],
                weight

            });


            wind.push({

                value:d.wind_speed_10m[hour],
                weight

            });


            direction.push({

                value:d.wind_direction_10m[hour],
                weight

            });


            codes.push({

                value:d.weather_code[hour],
                weight

            });

        });


        result.temperature_2m.push(
            weightedAverage(temperature)
        );

        result.relative_humidity_2m.push(
            weightedAverage(humidity)
        );

        result.apparent_temperature.push(
            weightedAverage(apparent)
        );

        result.precipitation.push(
            weightedAverage(precipitation)
        );

        result.precipitation_probability.push(
            weightedAverage(probability)
        );

        result.snowfall.push(
            weightedAverage(snowfall)
        );

        result.cloud_cover.push(
            weightedAverage(clouds)
        );

        result.wind_speed_10m.push(
            weightedAverage(wind)
        );

        result.wind_direction_10m.push(
            weightedWindDirection(direction)
        );

        result.weather_code.push(
            combinedWeatherCode(codes)
        );

    }


    return result;

}


/* =========================================================
   DATES
========================================================= */

const greekDays=[

    "Κυρ",
    "Δευ",
    "Τρί",
    "Τετ",
    "Πέμ",
    "Παρ",
    "Σάβ"

];


function formatDate(dateString){

    const parts =
        dateString.split("-");


    const year =
        Number(parts[0]);

    const month =
        Number(parts[1]);

    const day =
        Number(parts[2]);


    const date =
        new Date(
            Date.UTC(
                year,
                month-1,
                day
            )
        );


    return {

        day:
            greekDays[
                date.getUTCDay()
            ],

        date:
            `${day}/${month}`

    };

}


/* =========================================================
   SEARCH
========================================================= */

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

            Αναζήτηση τοποθεσίας...

        </div>`;


    try{

        const geoUrl =

            "https://geocoding-api.open-meteo.com/v1/search" +

            "?name=" +
            encodeURIComponent(city) +

            "&count=1" +

            "&language=el" +

            "&format=json";


        const response =
            await fetch(
                geoUrl,
                {
                    cache:"no-store"
                }
            );


        if(!response.ok)
            throw new Error("Geocoding failed");


        const geo =
            await response.json();


        if(
            !geo.results ||
            !geo.results.length
        ){

            alert(
                "Δεν βρέθηκε η πόλη."
            );

            return;

        }


        const place =
            geo.results[0];


        locationData={

            name:
                place.name,

            latitude:
                place.latitude,

            longitude:
                place.longitude,

            country:
                place.country,

            countryCode:
                place.country_code

        };


        await loadWeather();


    }catch(error){

        console.error(error);


        document
            .getElementById("forecast")
            .innerHTML =

            `<div class="loading">

                Σφάλμα αναζήτησης.

            </div>`;

    }

}


/* =========================================================
   MAIN WEATHER LOADER
========================================================= */

async function loadWeather(){

    if(!locationData)
        return;


    if(loadingRequest)
        return;


    loadingRequest=true;


    try{

        const lat =
            locationData.latitude;

        const lon =
            locationData.longitude;


        const common =

            "latitude=" +
            encodeURIComponent(lat) +

            "&longitude=" +
            encodeURIComponent(lon) +

            "&timezone=auto" +

            "&forecast_days=15";


        const current =

            "temperature_2m," +
            "relative_humidity_2m," +
            "apparent_temperature," +
            "weather_code," +
            "wind_speed_10m," +
            "wind_direction_10m," +
            "is_day";


        const hourly =

            "temperature_2m," +
            "relative_humidity_2m," +
            "apparent_temperature," +
            "precipitation," +
            "precipitation_probability," +
            "snowfall," +
            "weather_code," +
            "cloud_cover," +
            "wind_speed_10m," +
            "wind_direction_10m," +
            "is_day";


        const daily =

            "temperature_2m_max," +
            "temperature_2m_min," +
            "weather_code," +
            "precipitation_sum," +
            "precipitation_probability_max," +
            "snowfall_sum," +
            "wind_speed_10m_max," +
            "sunrise," +
            "sunset";


        const base =

            "https://api.open-meteo.com/v1/forecast?" +

            common +

            "&current=" +
            current +

            "&hourly=" +
            hourly +

            "&daily=" +
            daily;


        /*
           Κύρια μοντέλα.

           IFS HRES
           ECMWF AIFS
           NOAA GFS
           DWD ICON
        */

        const urls={

            ecmwf:
                base +
                "&models=ecmwf_ifs025",

            aifs:
                base +
                "&models=ecmwf_aifs025",

            gfs:
                base +
                "&models=gfs_seamless",

            icon:
                base +
                "&models=icon_seamless"

        };


        const names =
            Object.keys(urls);


        const results =
            await Promise.allSettled(

                names.map(
                    async name=>{

                        const response =
                            await fetch(
                                urls[name],
                                {
                                    cache:"no-store"
                                }
                            );


                        if(!response.ok){

                            throw new Error(
                                name +
                                " HTTP " +
                                response.status
                            );

                        }


                        const data =
                            await response.json();


                        return {

                            name,
                            data

                        };

                    }
                )

            );


        weatherData={};


        results.forEach(result=>{

            if(
                result.status==="fulfilled" &&
                result.value.data
            ){

                weatherData[
                    result.value.name
                ] =
                    result.value.data;

            }

        });


        /*
           Αν υπάρχει τουλάχιστον ένα μοντέλο,
           συνεχίζουμε.

           Δεν αποτυγχάνει ολόκληρη η σελίδα
           επειδή κάποιο μοντέλο καθυστέρησε.
        */

        if(!availableModels().length){

            throw new Error(
                "No model returned data"
            );

        }


        renderCurrent();

        renderForecast();


    }catch(error){

        console.error(
            "Forecast error:",
            error
        );


        document
            .getElementById("forecast")
            .innerHTML =

            `<div class="loading">

                Δεν ήταν δυνατή η φόρτωση
                δεδομένων καιρού.

                <br><br>

                Δοκίμασε ξανά.

            </div>`;

    }finally{

        loadingRequest=false;

    }

}


/* =========================================================
   CURRENT
========================================================= */

function renderCurrent(){

    const d =
        getBlendedCurrent();


    if(!d)
        return;


    const temp =
        d.temperature;

    const humidity =
        d.humidity;

    const wind =
        d.wind;

    const feels =
        d.apparent;

    const code =
        d.weatherCode;

    const direction =
        windDirection(
            d.windDirection
        );


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

                ${weatherIcon(
                    code,
                    d.isDay
                )}

                ${weatherText(code)}

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
                        ${direction}

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


/* =========================================================
   15 DAY FORECAST
========================================================= */

function renderForecast(){

    const d =
        getBlendedDaily();


    if(!d)
        return;


    let html="";


    for(
        let i=0;
        i<d.time.length;
        i++
    ){

        const date =
            formatDate(
                d.time[i]
            );


        const rain =
            Number(
                d.precipitation_probability_max[i]
                ||0
            );


        const snow =
            Number(
                d.snowfall_sum[i]
                ||0
            );


        /*
           Κρατάμε τη λογική:
           💧 κανονικός υετός
           ❄️ όταν υπάρχει χιόνι
        */

        let precipitationInfo =
            `💧 ${Math.round(rain)}%`;


        if(snow>0){

            precipitationInfo =
                `❄️ ${Math.round(rain)}%`;

        }


        html += `

        <div
            class="day"
            onclick="showHourly(${i})">

            <div class="day-name">

                ${date.day}

            </div>


            <div class="date">

                ${date.date}

            </div>


            <div class="icon">

                ${weatherIcon(
                    d.weather_code[i],
                    true,
                    rain,
                    snow
                )}

            </div>


            <div class="max">

                ${Math.round(
                    d.temperature_2m_max[i]
                )}°

            </div>


            <div class="min">

                ${Math.round(
                    d.temperature_2m_min[i]
                )}°

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


/* =========================================================
   HOURLY
========================================================= */

function showHourly(dayIndex){

    const d =
        getBlendedHourly();


    const daily =
        weatherData.ecmwf.daily;


    const date =
        daily.time[dayIndex];


    const rows=[];


    for(
        let i=0;
        i<d.time.length;
        i++
    ){

        if(
            d.time[i].startsWith(date)
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


    let html="";


    rows.forEach(i=>{

        const hour =
            d.time[i]
            .substring(11,16);


        const temp =
            Math.round(
                d.temperature_2m[i]
            );


        const feels =
            Math.round(
                d.apparent_temperature[i]
            );


        const rain =
            Math.round(
                d.precipitation_probability[i]
                ||0
            );


        const snowfall =
            Number(
                d.snowfall[i]
                ||0
            );


        const wind =
            Math.round(
                d.wind_speed_10m[i]
            );


        const direction =
            windDirection(
                d.wind_direction_10m[i]
            );


        const clouds =
            Math.round(
                d.cloud_cover[i]
            );


        const icon =
            weatherIcon(
                d.weather_code[i],
                d.is_day[i]===1,
                rain,
                snowfall
            );


        let precipitationHTML =
            `💧 ${rain}%`;


        if(snowfall>0){

            precipitationHTML =
                `❄️ ${rain}%`;

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
                <b>${temp}°</b>

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
                    ${direction}
                </b>

            </div>

        </div>

        `;

    });


    document
        .getElementById("hourly")
        .innerHTML =
        html;


    const section =
        document.getElementById(
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


/* =========================================================
   ΑΥΤΟΜΑΤΗ ΑΝΑΝΕΩΣΗ
========================================================= */

/*
   Κάνει νέο request κάθε 5 λεπτά.

   cache:"no-store" παραπάνω αποτρέπει
   την απλή χρήση παλιού browser cache.

   Το νέο request παίρνει ό,τι πιο πρόσφατο
   έχει ήδη δημοσιευτεί από τα μοντέλα.
*/

function startAutoRefresh(){

    if(refreshTimer){

        clearInterval(
            refreshTimer
        );

    }


    refreshTimer =
        setInterval(
            function(){

                if(
                    locationData &&
                    !document.hidden
                ){

                    loadWeather();

                }

            },
            5*60*1000
        );

}


document.addEventListener(
    "visibilitychange",
    function(){

        if(
            !document.hidden &&
            locationData
        ){

            loadWeather();

        }

    }
);


/* =========================================================
   CLICK OUTSIDE MENU
========================================================= */

document.addEventListener(
    "click",
    function(event){

        const menu =
            document.getElementById(
                "menu"
            );

        const button =
            document.querySelector(
                ".menu-button"
            );


        if(
            menu.classList.contains("open") &&
            !menu.contains(event.target) &&
            !button.contains(event.target)
        ){

            menu.classList.remove("open");

        }

    }
);


/* =========================================================
   ENTER SEARCH
========================================================= */

document
    .getElementById("cityInput")
    .addEventListener(
        "keydown",
        function(event){

            if(event.key==="Enter"){

                searchCity();

            }

        }
    );


/* =========================================================
   START
========================================================= */

searchCity();

startAutoRefresh();

</script>

</body>
</html>

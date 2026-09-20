<script>

let weatherData = null;
let locationData = null;
let historyYears = 1;


/* =========================================================
   ΜΕΝΟΥ
========================================================= */

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


/* =========================================================
   ΙΣΤΟΡΙΚΟ
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


/* =========================================================
   ΚΛΕΙΣΙΜΟ MENU ΜΕ CLICK ΕΞΩ
========================================================= */

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


/* =========================================================
   ΣΗΜΑΙΑ
========================================================= */

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


/* =========================================================
   WEATHER ICON
   ΚΡΑΤΗΜΕΝΗ Η ΔΙΚΗ ΣΟΥ ΛΟΓΙΚΗ
========================================================= */

function weatherIcon(
    code,
    isDay = true,
    precipitationProbability = 0,
    snowfall = 0
){

    const rain =
        Number(
            precipitationProbability || 0
        );

    const snow =
        Number(
            snowfall || 0
        );


    if(rain < 30){

        if(code === 0){

            if(isDay){

                return "☀️";

            }

            return '<span class="night-moon">🌙</span>';

        }


        if(code === 1){

            if(isDay){

                return "🌤️";

            }

            return '<span class="night-moon">🌙</span>';

        }


        if(code === 2){

            if(isDay){

                return "🌤️";

            }

            return `
                <span
                    class="night-partly-cloudy"
                    aria-label="Λίγες νεφώσεις τη νύχτα">
                </span>
            `;

        }


        if(code === 3){

            return "☁️";

        }


        if(
            [45,48].includes(code)
        ){

            return "🌫️";

        }


        if(
            [
                51,53,55,56,57,
                61,63,65,66,67,
                71,73,75,77,
                80,81,82,
                85,86,
                95,96,99
            ].includes(code)
        ){

            return "☁️";

        }


        if(isDay){

            return "🌤️";

        }

        return '<span class="night-moon">🌙</span>';

    }


    if(
        [95,96,99].includes(code)
    ){

        return "⛈️";

    }


    if(
        snow > 0 ||
        [
            71,73,75,77,
            85,86
        ].includes(code)
    ){

        return "🌨️";

    }


    if(
        [
            51,53,55,56,57,
            61,63,65,66,67,
            80,81,82
        ].includes(code)
    ){

        return "🌧️";

    }


    return "🌧️";

}


/* =========================================================
   WEATHER TEXT
========================================================= */

function weatherText(code){

    if(code === 0)
        return "Αίθριος";

    if(code === 1)
        return "Κυρίως αίθριος";

    if(code === 2)
        return "Λίγες νεφώσεις";

    if(code === 3)
        return "Συννεφιά";

    if(
        [45,48].includes(code)
    )
        return "Ομίχλη";

    if(
        [51,53,55,56,57].includes(code)
    )
        return "Ψιλόβροχο";

    if(
        [61,63,65].includes(code)
    )
        return "Βροχή";

    if(
        [66,67].includes(code)
    )
        return "Χιονόνερο";

    if(
        [71,73,75,77].includes(code)
    )
        return "Χιόνι";

    if(
        [80,81,82].includes(code)
    )
        return "Μπόρες";

    if(
        [85,86].includes(code)
    )
        return "Χιονομπόρες";

    if(
        [95,96,99].includes(code)
    )
        return "Καταιγίδα";

    return "Μεταβλητός καιρός";

}


/* =========================================================
   ΑΝΕΜΟΣ
========================================================= */

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


/* =========================================================
   ΜΕΣΟΣ ΟΡΟΣ ΜΟΝΤΕΛΩΝ
========================================================= */

/*
   Τα βάρη ΔΕΝ είναι βάρη του TWC.
   Είναι πρακτικός multi-model συνδυασμός.

   IFS HRES  = 40%
   AIFS      = 25%
   GFS       = 20%
   ICON      = 15%

   Όταν ένα μοντέλο λείπει για κάποια ώρα/ημέρα,
   τα βάρη των διαθέσιμων μοντέλων
   κανονικοποιούνται αυτόματα.
*/


const MODEL_WEIGHTS = {

    ecmwf: 0.40,

    aifs: 0.25,

    gfs: 0.20,

    icon: 0.15

};


/* =========================================================
   ΑΣΦΑΛΗΣ ΑΡΙΘΜΗΤΙΚΟΣ ΜΕΣΟΣ
========================================================= */

function weightedAverage(values){

    let total = 0;
    let weightTotal = 0;


    values.forEach(item => {

        const value =
            Number(item.value);

        const weight =
            Number(item.weight);


        if(
            Number.isFinite(value) &&
            Number.isFinite(weight)
        ){

            total +=
                value * weight;

            weightTotal +=
                weight;

        }

    });


    if(weightTotal === 0){

        return null;

    }


    return total / weightTotal;

}


/* =========================================================
   ΚΥΚΛΙΚΟΣ ΜΕΣΟΣ ΓΙΑ ΔΙΕΥΘΥΝΣΗ ΑΝΕΜΟΥ
========================================================= */

function weightedWindDirection(items){

    let sinTotal = 0;
    let cosTotal = 0;
    let weightTotal = 0;


    items.forEach(item => {

        const degrees =
            Number(item.value);

        const weight =
            Number(item.weight);


        if(
            !Number.isFinite(degrees) ||
            !Number.isFinite(weight)
        ){

            return;

        }


        const radians =
            degrees * Math.PI / 180;


        sinTotal +=
            Math.sin(radians) * weight;

        cosTotal +=
            Math.cos(radians) * weight;

        weightTotal +=
            weight;

    });


    if(weightTotal === 0){

        return null;

    }


    let degrees =
        Math.atan2(
            sinTotal,
            cosTotal
        ) * 180 / Math.PI;


    if(degrees < 0){

        degrees += 360;

    }


    return degrees;

}


/* =========================================================
   MODE / ΣΥΝΔΥΑΣΜΟΣ WEATHER CODES
========================================================= */

function combinedWeatherCode(items){

    const scores = {};


    items.forEach(item => {

        const code =
            Number(item.value);

        const weight =
            Number(item.weight);


        if(
            !Number.isFinite(code) ||
            !Number.isFinite(weight)
        ){

            return;

        }


        scores[code] =
            (scores[code] || 0) +
            weight;

    });


    let bestCode = 0;
    let bestScore = -1;


    Object.keys(scores).forEach(code => {

        if(scores[code] > bestScore){

            bestScore =
                scores[code];

            bestCode =
                Number(code);

        }

    });


    return bestCode;

}


/* =========================================================
   ΕΝΑ ΜΟΝΤΕΛΟ ΣΤΟ BLEND
========================================================= */

function getModelWeight(name){

    return MODEL_WEIGHTS[name] || 0;

}


function availableModels(){

    const models = [];


    if(weatherData.ecmwf){

        models.push("ecmwf");

    }


    if(weatherData.aifs){

        models.push("aifs");

    }


    if(weatherData.gfs){

        models.push("gfs");

    }


    if(weatherData.icon){

        models.push("icon");

    }


    return models;

}


/* =========================================================
   BLENDED CURRENT
========================================================= */

function getBlendedCurrent(){

    const models =
        availableModels();


    if(!models.length){

        return null;

    }


    const temperature = [];

    const humidity = [];
    const apparent = [];
    const wind = [];
    const direction = [];


    models.forEach(name => {

        const d =
            weatherData[name];


        if(!d || !d.current){

            return;

        }


        const weight =
            getModelWeight(name);


        temperature.push({

            value:
                d.current.temperature_2m,

            weight

        });


        humidity.push({

            value:
                d.current.relative_humidity_2m,

            weight

        });


        apparent.push({

            value:
                d.current.apparent_temperature,

            weight

        });


        wind.push({

            value:
                d.current.wind_speed_10m,

            weight

        });


        direction.push({

            value:
                d.current.wind_direction_10m,

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
            combinedWeatherCode(
                models.map(name => ({

                    value:
                        weatherData[name]
                        .current
                        .weather_code,

                    weight:
                        getModelWeight(name)

                }))
            ),

        isDay:
            weatherData.ecmwf &&
            weatherData.ecmwf.current
            .is_day === 1

    };

}


/* =========================================================
   BLENDED DAILY
========================================================= */

function getBlendedDaily(){

    const base =
        weatherData.ecmwf.daily;


    const result = {

        time:
            base.time.slice(),

        temperature_2m_max: [],

        temperature_2m_min: [],

        weather_code: [],

        precipitation_probability_max: [],

        snowfall_sum: [],

        precipitation_sum: [],

        wind_speed_10m_max: [],

        sunrise:
            base.sunrise,

        sunset:
            base.sunset

    };


    for(
        let day = 0;
        day < base.time.length;
        day++
    ){

        const tempMax = [];
        const tempMin = [];
        const precipProb = [];
        const snow = [];
        const precip = [];
        const windMax = [];
        const codes = [];


        availableModels().forEach(name => {

            const d =
                weatherData[name].daily;


            if(
                !d ||
                !d.time ||
                day >= d.time.length
            ){

                return;

            }


            const weight =
                getModelWeight(name);


            tempMax.push({

                value:
                    d.temperature_2m_max[day],

                weight

            });


            tempMin.push({

                value:
                    d.temperature_2m_min[day],

                weight

            });


            precipProb.push({

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


            windMax.push({

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

            weightedAverage(tempMax)

        );


        result.temperature_2m_min.push(

            weightedAverage(tempMin)

        );


        result.precipitation_probability_max.push(

            weightedAverage(precipProb)

        );


        result.snowfall_sum.push(

            weightedAverage(snow)

        );


        result.precipitation_sum.push(

            weightedAverage(precip)

        );


        result.wind_speed_10m_max.push(

            weightedAverage(windMax)

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


    const result = {

        time:
            base.time.slice(),

        temperature_2m: [],

        relative_humidity_2m: [],

        apparent_temperature: [],

        precipitation: [],

        precipitation_probability: [],

        snowfall: [],

        weather_code: [],

        cloud_cover: [],

        wind_speed_10m: [],

        wind_direction_10m: [],

        is_day:
            base.is_day.slice()

    };


    for(
        let hour = 0;
        hour < base.time.length;
        hour++
    ){

        const temperature = [];
        const humidity = [];
        const apparent = [];
        const precipitation = [];
        const precipProbability = [];
        const snowfall = [];
        const cloud = [];
        const wind = [];
        const direction = [];
        const codes = [];


        availableModels().forEach(name => {

            const d =
                weatherData[name].hourly;


            if(
                !d ||
                !d.time ||
                hour >= d.time.length
            ){

                return;

            }


            /*
              Τα μοντέλα έχουν ίδια hourly χρονική
              βάση από το Open-Meteo API.
            */

            const weight =
                getModelWeight(name);


            temperature.push({

                value:
                    d.temperature_2m[hour],

                weight

            });


            humidity.push({

                value:
                    d.relative_humidity_2m[hour],

                weight

            });


            apparent.push({

                value:
                    d.apparent_temperature[hour],

                weight

            });


            precipitation.push({

                value:
                    d.precipitation[hour],

                weight

            });


            precipProbability.push({

                value:
                    d.precipitation_probability[hour],

                weight

            });


            snowfall.push({

                value:
                    d.snowfall[hour],

                weight

            });


            cloud.push({

                value:
                    d.cloud_cover[hour],

                weight

            });


            wind.push({

                value:
                    d.wind_speed_10m[hour],

                weight

            });


            direction.push({

                value:
                    d.wind_direction_10m[hour],

                weight

            });


            codes.push({

                value:
                    d.weather_code[hour],

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

            weightedAverage(precipProbability)

        );


        result.snowfall.push(

            weightedAverage(snowfall)

        );


        result.weather_code.push(

            combinedWeatherCode(codes)

        );


        result.cloud_cover.push(

            weightedAverage(cloud)

        );


        result.wind_speed_10m.push(

            weightedAverage(wind)

        );


        result.wind_direction_10m.push(

            weightedWindDirection(direction)

        );

    }


    return result;

}


/* =========================================================
   ΗΜΕΡΕΣ ΕΛΛΗΝΙΚΑ
========================================================= */

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


/* =========================================================
   ΑΝΑΖΗΤΗΣΗ ΠΟΛΗΣ
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


    document
        .getElementById("forecast")
        .innerHTML =

        `<div class="loading">

            Αναζήτηση πόλης...

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
            await fetch(geoUrl);


        if(!response.ok){

            throw new Error(
                "Geocoding failed"
            );

        }


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


        locationData = {

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

                Σφάλμα φόρτωσης δεδομένων.

             </div>`;

    }

}


/* =========================================================
   WEATHER LOADER
   ΝΕΟ MULTI-MODEL SYSTEM
========================================================= */

async function loadWeather(){

    const lat =
        locationData.latitude;


    const lon =
        locationData.longitude;


    document
        .getElementById("current")
        .innerHTML = `

        <div class="current">

            <div class="loading">

                Λήψη τελευταίων δεδομένων
                πολλαπλών μοντέλων...

            </div>

        </div>

    `;


    document
        .getElementById("forecast")
        .innerHTML =

        `<div class="loading">

            Υπολογισμός πρόγνωσης...

        </div>`;


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


    /*
       Τα μοντέλα που χρησιμοποιούμε:

       ECMWF IFS HRES
       ECMWF AIFS
       NOAA GFS
       DWD ICON
    */


    const urls = {

        ecmwf:

            "https://api.open-meteo.com/v1/forecast?" +

            common +

            "&current=" +
            current +

            "&hourly=" +
            hourly +

            "&daily=" +
            daily +

            "&models=ecmwf_ifs025",


        aifs:

            "https://api.open-meteo.com/v1/forecast?" +

            common +

            "&current=" +
            current +

            "&hourly=" +
            hourly +

            "&daily=" +
            daily +

            "&models=ecmwf_aifs025",


        gfs:

            "https://api.open-meteo.com/v1/forecast?" +

            common +

            "&current=" +
            current +

            "&hourly=" +
            hourly +

            "&daily=" +
            daily +

            "&models=gfs_seamless",


        icon:

            "https://api.open-meteo.com/v1/forecast?" +

            common +

            "&current=" +
            current +

            "&hourly=" +
            hourly +

            "&daily=" +
            daily +

            "&models=icon_seamless"

    };


    try{

        const entries =
            Object.entries(urls);


        const responses =
            await Promise.all(

                entries.map(
                    ([name,url]) =>
                        fetch(url)
                        .then(response => {

                            if(!response.ok){

                                throw new Error(
                                    name +
                                    " request failed"
                                );

                            }

                            return response.json();

                        })
                        .then(data => ({

                            name,
                            data

                        }))
                )

            );


        weatherData = {};


        responses.forEach(item => {

            weatherData[item.name] =
                item.data;

        });


        /*
           Αν κάποιο μοντέλο δεν επιστρέψει δεδομένα,
           συνεχίζουμε με τα υπόλοιπα.
        */

        if(
            !weatherData.ecmwf ||
            !weatherData.ecmwf.daily
        ){

            throw new Error(
                "ECMWF data unavailable"
            );

        }


        renderCurrent();

        renderForecast();


    }catch(error){

        console.error(
            "Multi-model forecast error:",
            error
        );


        /*
           FALLBACK:
           Αν αποτύχει το multi-model request,
           ζητάμε το Best Match του Open-Meteo.
        */

        try{

            const fallbackUrl =

                "https://api.open-meteo.com/v1/forecast?" +

                common +

                "&current=" +
                current +

                "&hourly=" +
                hourly +

                "&daily=" +
                daily;


            const fallbackResponse =
                await fetch(fallbackUrl);


            if(!fallbackResponse.ok){

                throw new Error(
                    "Fallback failed"
                );

            }


            const fallback =
                await fallbackResponse.json();


            weatherData = {

                ecmwf:
                    fallback

            };


            renderCurrent();

            renderForecast();


        }catch(fallbackError){

            console.error(
                fallbackError
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

        }

    }

}


/* =========================================================
   ΤΡΕΧΩΝ ΚΑΙΡΟΣ
========================================================= */

function renderCurrent(){

    const d =
        getBlendedCurrent();


    if(!d){

        return;

    }


    const temp =
        d.temperature;


    const humidity =
        d.humidity;


    const wind =
        d.wind;


    const windDir =
        windDirection(
            d.windDirection
        );


    const feels =
        d.apparent;


    const code =
        d.weatherCode;


    const isDay =
        d.isDay;


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
                    isDay
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


/* =========================================================
   15 ΗΜΕΡΕΣ
========================================================= */

function renderForecast(){

    const d =
        getBlendedDaily();


    let html = "";


    for(
        let i = 0;
        i < d.time.length;
        i++
    ){

        const date =
            formatDate(
                d.time[i]
            );


        const rain =
            Number(
                d.precipitation_probability_max[i]
                || 0
            );


        const snow =
            Number(
                d.snowfall_sum[i]
                || 0
            );


        /*
           💧 Πάντα υετός.
           ❄️ μόνο όταν υπάρχει χιόνι.
        */

        let precipitationInfo =
            `💧 ${Math.round(rain)}%`;


        if(snow > 0){

            precipitationInfo =
                `❄️ ${Math.round(rain)}%`;

        }


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
   ΩΡΙΑΙΑ
========================================================= */

function showHourly(dayIndex){

    const d =
        getBlendedHourly();


    const date =
        weatherData
        .ecmwf
        .daily
        .time[dayIndex];


    const rows = [];


    for(
        let i = 0;
        i < d.time.length;
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


    let html = "";


    rows.forEach(i => {

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
                || 0
            );


        const snowfall =
            Number(
                d.snowfall[i]
                || 0
            );


        const wind =
            Math.round(
                d.wind_speed_10m[i]
            );


        const windDir =
            windDirection(
                d.wind_direction_10m[i]
            );


        const clouds =
            Math.round(
                d.cloud_cover[i]
            );


        const isDay =
            d.is_day[i] === 1;


        const icon =
            weatherIcon(
                d.weather_code[i],
                isDay,
                rain,
                snowfall
            );


        let precipitationHTML = "";


        if(snowfall > 0){

            precipitationHTML = `

                ❄️ ${rain}%

            `;

        }else{

            precipitationHTML = `

                💧 ${rain}%

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


/* =========================================================
   ENTER ΣΤΗΝ ΑΝΑΖΗΤΗΣΗ
========================================================= */

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


/* =========================================================
   ΕΝΑΡΞΗ
========================================================= */

searchCity();

</script>

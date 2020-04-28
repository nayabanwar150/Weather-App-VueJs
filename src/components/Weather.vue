<template>
    <div class="weather">
        <div class="search-box">
            <form  @submit="fetchWeather">
                <input type="text" name="city" placeholder="Find Your City..." v-model="search_city">
            </form>
        </div>
        <div class="weather-wrap"  v-if="typeof weather.main != 'undefined'">
            <div class="location-box">
                <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
                <div class="date">{{dateBuilder()}}</div>
            </div>
            <div class="temp-box">
                <div class="temp">{{Math.round((weather.main.temp)-273.15)}}°C</div>
                <div class="weather-type">{{weather.weather[0].main}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Weather",
    props: ["weather"],
    data(){
        return{
            search_city: ''
        }
    },
    methods:{
        fetchWeather(e){
            e.preventDefault();
            let  search_city = this.search_city;
            this.$emit('search', search_city);
        },
        dateBuilder(){
            let d = new Date();
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return `${day} ${date} ${month} ${year}`
        }
    }
}
</script>

<style scoped>
    .weather{
        padding: 25px;
        min-height: 100vh;
        background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
    }

    .search-box{
        width: 100%;
        margin-bottom: 30px;
    }
    input[type="text"]{
        display: block;
        text-align: center;
        color: #313131;
        width: 100%;
        padding: 15px;
        border-radius: 0px 16px 0px 16px;
        appearance: none;
        border: none;
        outline: none;
        background: none;
        background-color: rgba(255,255,255,0.5);
        box-shadow: 0px 0px 8px rgba(0,0,0,0.25) ;
        transition: 0.4s;
    }

    input[type="text"]:focus{
        background-color: rgba(255,255,255,0.75);
        border-radius: 16px 0px 16px 0px;
        box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
        border: 1px solid rgb(218, 17, 34);
    }

    .location-box .location{
        color: #fff;
        font-size: 32px;
        font-weight: 500;
        text-align: center;
        text-shadow: 1px 3px rgba(0,0,0,0.25);
    }

    .location-box .date{
        color: #cec7c7;
        font-size: 20px;
        font-weight: 300;
        font-style: italic;
        text-align: center;
    }

    .weather-wrap{
        text-align: center;
    }
    
    .temp-box .temp{
        display: inline-block;
        padding: 10px 25px;
        color: #fff;
        font-size: 102px;
        font-weight: 900;
        text-shadow: 3px 6px rgba(0,0,0,0.25);
        background-color: rgba(255, 255, 255, 0.25);
        border-radius: 16px;
        margin: 30px 0px;
        box-shadow: 3px 6px rgba(0,0,0,0.25);
    }

    .temp-box .weather-type{
        color: #fff;
        font-size: 48px;
        font-weight: 700;
        font-style: italic;
        text-shadow: 3px 6px rgba(0,0,0,0.25);
    }
</style>
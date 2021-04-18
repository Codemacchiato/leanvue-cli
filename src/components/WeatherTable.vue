<template>
    <div class="container">
        <div class="m-3" v-cloak>
            <h1>Welcome to {{title}}</h1>
        </div>
        <table class="table table-bordered">
            <thead>
                <th>No</th>
                <th>Area</th>
                <th>Weather</th>
                <th>Action</th>
            </thead>

            <tbody is="transition-group" name="list" >
                <tr v-for="(item, index) in weatherData"
                    :class="{ 'table-danger' : isDanger(item.forecast) } "
                    v-bind:key="item.area">
                    <td>{{index + 1}}</td>
                    <td>{{item.area}}</td>
                    <td>{{item.forecast}}
                        <i v-if="isShower(item.forecast)" class="fas fa-cloud-showers-heavy"></i>
                        <i v-else-if="item.forecast === 'Thundery Showers'" class="fas fa-bolt"></i>
                    </td>
                    <td><button type="button" class="btn btn-warning" @click="removeWeather(index)">Remove</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data: function () {
        return {
            title: "Singapore weather app!",
            weatherData : [],
            show: true
        }
    },
    created : function () {
        this.getWeatherInfo()
    },
    methods : {
        getWeatherInfo : function () {
            axios
                .get("https://api.data.gov.sg/v1/environment/2-hour-weather-forecast")
                .then (response => {
                    this.weatherData = response.data.items[0].forecasts
                })
        },
        isDanger : function(forecast){
            return forecast === "Showers"
        },
        removeWeather : function (index) {
            this.weatherData.splice(index, 1)
        },
        isShower : function(forecast) {
            return "Showers" === forecast
        }
    }
}
</script>

<style scoped>

    [v-cloak] {
        display: none;
    }
    .list-enter-active, .list-leave-active {
            transition: all 0.5s;
    }
    .list-enter, .list-leave-to {
        opacity: 0;
        transform: translateY(30px);
    }

</style>
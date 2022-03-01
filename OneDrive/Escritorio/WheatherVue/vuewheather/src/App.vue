<template>
	<div id="app">
		<main>
			<div class="search-box">
				<input type="text" class="search-bar" placeholder="Busca Ciudad" v-model="query" @keypress="fetchweather">
			</div>



			<div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
				<div class="location-box">
					<div class="location">{{weather.name}}, {{weather.sys.country}}</div>
					<div class="date">{{Fecha()}}</div>
				</div>

				<div class="weather-box">
					<div class="temp">{{weather.main.temp}}ºC</div>
					<div class="weather">{{weather.weather.main}}</div>
				</div>
			</div>
		</main>

	</div>
</template>

<script>
	export default {
		name: 'App',
		data() {
			return {
				api_key: "a8aae5986479300eb04c0f2abfe450f7",
				url_base: "http://api.openweathermap.org/data/2.5/weather",
				query: "",
				weather: {},
				
			}
		},

		methods: {
			fetchweather(e) {
				if (e.key == "Enter") {
					fetch(`${this.url_base}?q=${this.query}&units=metric&APPID=${this.api_key}`)
						.then(res => {
							return res.json();
						}).then(this.setResults)
				}
			},

			setResults(results) {
				this.weather = results;
			},
			
			Fecha(){
				const d = new Date();
				
				let months =["Enero","Febrero","Marzo","Abril","Mayo","Junio","Julio","Agosto","Septiembre","Octubre","Noviembre","Diciembre",];
				
				let days = ["Lunes","Martes","Miercoles","Jueves","Viernes","Sabado","Domingo",];
				
				let day = days[d.getDay()];
				let month = months[d.getMonth()];
				let date = d.getDate();
				
				return `${day} ${date} ${month}`
			}
		}
	}

</script>

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	body {
		font-family: 'verdana', sans-serif;
	}

	#app {
		background-image: url(assets/cold-bg.jpg);
		background-size: cover;
		background-position: bottom;
		transition: 0.4s;
	}

	main {
		min-height: 100vh;
		padding: 25px;

		background-image: linear-gradient(to bottom, rgba(0, 0, 0, .25), rgba(0, 0, 0, .75))
	}


	.search-box {
		width: 100%;
		margin-bottom: 30px
	}

	.search-box .search-bar {
		display: block;
		width: 100%;
		padding: 15px;
		color: #313131;


		box-shadow: 0px 0px 8px rgba(0, 0, 0, .25);
		font-size: 20px;
		border: none;
		appearance: none;
		outline: none;
		background: none;

		background-color: rgba(255, 255, 255, .5);
		border-radius: 0px 16px;
		transition: .4s;
	}

	.search-box .search-bar:focus {
		box-shadow: 0px 0px 16px rgba(0, 0, 0, .25);
		background-color: rgba(255, 255, 255, .75);
		border-radius: 16px 0px 16px 0px;
	}

	.location-box .location {
		color: white;
		font-size: 32px;
		font-weight: 500;
		text-align: center;
		text-shadow: 1px 3px rgba(0, 0, 0, .25);
	}

	.location-box .date {
		color: white;
		font-size: 32px;
		font-weight: 500;

		font-style: italic;
		text-align: center;
	}

	.weather-box {
		text-align: center;
	}


	.weather-box .temp {
		display: inline-block;
		padding: 10px 25px;
		color: white;
		font-size: 60px;
		font-weight: 900;

		text-shadow: 3px 6px rgba(0, 0, 0, .25);
		background-color: rgba(255, 255, 255, .25);

		border-radius: 16px;
		margin: 30px 0px;

		box-shadow: 3px 6px rgba(0, 0, 0, .25)
	}


	.weather-box .weather {
		color: white;
		font-size: 48px;
		font-weight: 700;
		font-style: italic;
		text-shadow: 3px 6px rgba(0, 0, 0, .25)
	}

</style>

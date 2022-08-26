# Weather-Android-Library
## how to use

You need an API Key to use the OpenWeatherMap API.

## Download

## Step 1. Add the JitPack repository to your root build.gradle file.

```sh
allprojects {
  repositories {
    maven { url 'https://jitpack.io' }
  }
}
```
 ## Step 2. Add the dependency
```sh
dependencies {
	        implementation 'com.github.rahul0007:Weather-Android-Library:1.0.0'
	}
```

## Usage


Instantiate Model calss With Your Api Key and other parameter  

## Example
```sh
val weatherRequestDate = WeatherRequestData(
            city = "cityname",
            currentWeather = true,
            apiKey = "apikey"
        )
```

        
        
and pass this model in intent to start wather Actvity and return currnt Temperature and WindSpeed in registerForActivityResult
## get current day weather 
```sh


private fun getCurrentWeather() {
        val intent = Intent(this, WeatherActivity::class.java)
        val weatherRequestDate = WeatherRequestData(
            city = "CityName",
            currentWeather = true,
            apiKey = "apiKey"
        )
        intent.putExtra("weatherRequestDate", weatherRequestDate)
        startForResult.launch(intent)
    }
```

total number of day weather list then add

## get total number of day weather list
```sh

private fun openActivityForResultLast7Days() {
        val intent = Intent(this, WeatherActivity::class.java)
        val weatherRequestDate = WeatherRequestData(
            city = "CityName",
            currentWeather = false,
            apiKey = "apiKey",
            lat = "37",
            log = "137",
            totalDays = "7"
        )
        intent.putExtra("weatherRequestDate", weatherRequestDate)
        startForResult.launch(intent)
    }
```
 
 ## you can get result inside of registerForActivityResult
 

```sh
 val startForResult =
        registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result: ActivityResult ->
            when (result.resultCode) {
                Activity.RESULT_OK -> {
                }
                SUCCESS_CURRENT_WEATHER_CODE -> {
                    val intent = result.data!!.extras!!.get("WeatherResult") as CurrentWeatherData
                    Log.e("intent.Temperature", "intent.Temperature" + intent.Temperature)
                    textViewTemperature.text = "Temperature: "+intent.Temperature
                    textViewWindSpeed.text = "WindSpeed: " +intent.WindSpeed
                    textViewTemperatureC.text = "TemperatureC: " +intent.TemperatureC
                    textViewTemperatureF.text = "TemperatureF: " +intent.TemperatureF
                }
                SUCCESS_LAST_7DAYS -> {
                    val last7Days =
                        result.data!!.extras!!.get("WeatherResult") as DayListWeatherData
                    Log.e("last7Days", "last7Days" + last7Days.city)
                }
            }
        }
```
**RS**




# Weather\-git\-scraping

Initialize

```matlab
apikey = getenv("OWM_KEY");
url = "https://api.openweathermap.org/data/2.5/weather?q=Boston&appid="+apikey;
% T = getWeather(url)
```

```matlab
% writetable(T,"weather_boston.csv")
```

Iterate

```matlab
T = readtable("weather_boston.csv")
```
| |temp|feels_like|temp_min|temp_max|pressure|humidity|sea_level|grnd_level|time|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|302.2400|305.7000|300.2900|303.3300|1004|68|1004|1001|20-Jul-2025 21:49:26|

```matlab
T2 = getWeather(url);
T = [T;T2];
writetable(T,"weather_boston.csv")
```

```matlab
function T = getWeather(url)
data = webread(url,weboptions(Timeout=10));
weather = data.main;
weather.time = datetime(data.dt,"ConvertFrom","posixtime");
T = struct2table(weather);
end
```

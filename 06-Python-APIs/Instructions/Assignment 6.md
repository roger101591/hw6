

```python
from citipy import citipy
import random 
import requests
import pandas as pd
import matplotlib.pyplot as plt
from config import api_key

cities = []
lat = []
lng = []
temp = []
humidity = []
wspeed = []
cloudiness = []
url = "http://api.openweathermap.org/data/2.5/weather?"
city_count = 0

```


```python
#test
latitude = random.uniform(-90, 90)
longitude = random.uniform(-180,180)
city = citipy.nearest_city(float("{0:.2f}".format(latitude)), float("{0:.2f}".format(longitude)) )
city = city.city_name
query_url = url + "appid=" + api_key + "&q=" + city + '&units=Imperial'
        
weather_response = requests.get(query_url)
weather_json = weather_response.json() 
weather_response
```




    <Response [200]>




```python
while len(cities) < 500:
    
        latitude = random.uniform(-90, 90)
        longitude = random.uniform(-180,180)
        city = citipy.nearest_city(float("{0:.2f}".format(latitude)), float("{0:.2f}".format(longitude)) )
        city = city.city_name
        
    # Build query URL
  
        query_url = url + "appid=" + api_key + "&q=" + city + '&units=Imperial'       
        weather_response = requests.get(query_url)
#get only data where json response is successful  
        if weather_response.status_code == 200: 
            weather_json = weather_response.json()
            
#get data for 500 unique cities
            if city not in cities:
                cities.append(city)
                
                lat.append("{0:.2f}".format(latitude))
                lng.append("{0:.2f}".format(longitude))
                temp.append(weather_json['main']['temp'])            
                humidity.append(weather_json['main']['humidity'])            
                wspeed.append(weather_json['wind']['speed'])           
                cloudiness.append(weather_json['clouds']['all'])
                print('City Number: ' + str(city_count) + ' City_Name: ' + city + ' Query_URL: ' + str(query_url))
                city_count = city_count + 1
weatherDF = pd.DataFrame({'Cities': cities, 'Temp': temp, 'Humidity': humidity, "Wind Speed": wspeed, 'Cloudiness':cloudiness, 'Latitude': lat, 'Longitude': lng})


#weatherDF = weatherDF.loc[weatherDF.loc[:, 'Temp'] != 'NA', :]
print(len(weatherDF))
```

    City Number: 0 City_Name: rikitea Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=rikitea&units=Imperial
    City Number: 1 City_Name: hobart Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hobart&units=Imperial
    City Number: 2 City_Name: kaduqli Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kaduqli&units=Imperial
    City Number: 3 City_Name: cairns Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cairns&units=Imperial
    City Number: 4 City_Name: tezu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tezu&units=Imperial
    City Number: 5 City_Name: avarua Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=avarua&units=Imperial
    City Number: 6 City_Name: butaritari Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=butaritari&units=Imperial
    City Number: 7 City_Name: neuquen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=neuquen&units=Imperial
    City Number: 8 City_Name: ushuaia Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ushuaia&units=Imperial
    City Number: 9 City_Name: kapaa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kapaa&units=Imperial
    City Number: 10 City_Name: severo-kurilsk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=severo-kurilsk&units=Imperial
    City Number: 11 City_Name: bilibino Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bilibino&units=Imperial
    City Number: 12 City_Name: teya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=teya&units=Imperial
    City Number: 13 City_Name: ouesso Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ouesso&units=Imperial
    City Number: 14 City_Name: port alfred Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port alfred&units=Imperial
    City Number: 15 City_Name: santa maria Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=santa maria&units=Imperial
    City Number: 16 City_Name: salinopolis Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=salinopolis&units=Imperial
    City Number: 17 City_Name: vardo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vardo&units=Imperial
    City Number: 18 City_Name: punta arenas Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=punta arenas&units=Imperial
    City Number: 19 City_Name: mataura Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mataura&units=Imperial
    City Number: 20 City_Name: aswan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aswan&units=Imperial
    City Number: 21 City_Name: kahului Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kahului&units=Imperial
    City Number: 22 City_Name: nome Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nome&units=Imperial
    City Number: 23 City_Name: vila franca do campo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vila franca do campo&units=Imperial
    City Number: 24 City_Name: tasiilaq Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tasiilaq&units=Imperial
    City Number: 25 City_Name: khatanga Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=khatanga&units=Imperial
    City Number: 26 City_Name: ribeira grande Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ribeira grande&units=Imperial
    City Number: 27 City_Name: sao filipe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sao filipe&units=Imperial
    City Number: 28 City_Name: cidreira Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cidreira&units=Imperial
    City Number: 29 City_Name: bassar Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bassar&units=Imperial
    City Number: 30 City_Name: halifax Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=halifax&units=Imperial
    City Number: 31 City_Name: bethel Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bethel&units=Imperial
    City Number: 32 City_Name: lazaro cardenas Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lazaro cardenas&units=Imperial
    City Number: 33 City_Name: harper Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=harper&units=Imperial
    City Number: 34 City_Name: atuona Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=atuona&units=Imperial
    City Number: 35 City_Name: coquimbo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=coquimbo&units=Imperial
    City Number: 36 City_Name: leningradskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=leningradskiy&units=Imperial
    City Number: 37 City_Name: arraial do cabo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=arraial do cabo&units=Imperial
    City Number: 38 City_Name: lebu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lebu&units=Imperial
    City Number: 39 City_Name: pangody Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pangody&units=Imperial
    City Number: 40 City_Name: bismarck Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bismarck&units=Imperial
    City Number: 41 City_Name: vestmanna Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vestmanna&units=Imperial
    City Number: 42 City_Name: qaanaaq Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=qaanaaq&units=Imperial
    City Number: 43 City_Name: nakhon thai Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nakhon thai&units=Imperial
    City Number: 44 City_Name: lamas Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lamas&units=Imperial
    City Number: 45 City_Name: port lincoln Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port lincoln&units=Imperial
    City Number: 46 City_Name: shaunavon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=shaunavon&units=Imperial
    City Number: 47 City_Name: luderitz Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=luderitz&units=Imperial
    City Number: 48 City_Name: albany Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=albany&units=Imperial
    City Number: 49 City_Name: cape town Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cape town&units=Imperial
    City Number: 50 City_Name: baykit Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=baykit&units=Imperial
    City Number: 51 City_Name: yellowknife Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yellowknife&units=Imperial
    City Number: 52 City_Name: kruisfontein Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kruisfontein&units=Imperial
    City Number: 53 City_Name: quelimane Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=quelimane&units=Imperial
    City Number: 54 City_Name: fortuna Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=fortuna&units=Imperial
    City Number: 55 City_Name: touros Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=touros&units=Imperial
    City Number: 56 City_Name: talnakh Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=talnakh&units=Imperial
    City Number: 57 City_Name: makakilo city Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=makakilo city&units=Imperial
    City Number: 58 City_Name: lompoc Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lompoc&units=Imperial
    City Number: 59 City_Name: anadyr Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=anadyr&units=Imperial
    City Number: 60 City_Name: krathum baen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=krathum baen&units=Imperial
    City Number: 61 City_Name: broken hill Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=broken hill&units=Imperial
    City Number: 62 City_Name: nhulunbuy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nhulunbuy&units=Imperial
    City Number: 63 City_Name: sitka Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sitka&units=Imperial
    City Number: 64 City_Name: busselton Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=busselton&units=Imperial
    City Number: 65 City_Name: vaini Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vaini&units=Imperial
    City Number: 66 City_Name: puerto ayora Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=puerto ayora&units=Imperial
    City Number: 67 City_Name: dzilam gonzalez Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dzilam gonzalez&units=Imperial
    City Number: 68 City_Name: lyaskelya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lyaskelya&units=Imperial
    City Number: 69 City_Name: storforshei Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=storforshei&units=Imperial
    City Number: 70 City_Name: jumla Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=jumla&units=Imperial
    City Number: 71 City_Name: mahebourg Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mahebourg&units=Imperial
    City Number: 72 City_Name: dikson Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dikson&units=Imperial
    City Number: 73 City_Name: valdivia Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=valdivia&units=Imperial
    City Number: 74 City_Name: khani Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=khani&units=Imperial
    City Number: 75 City_Name: hasaki Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hasaki&units=Imperial
    City Number: 76 City_Name: san cristobal Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san cristobal&units=Imperial
    City Number: 77 City_Name: nelson bay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nelson bay&units=Imperial
    City Number: 78 City_Name: georgetown Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=georgetown&units=Imperial
    City Number: 79 City_Name: atocha Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=atocha&units=Imperial
    City Number: 80 City_Name: masakin Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=masakin&units=Imperial
    City Number: 81 City_Name: barsovo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=barsovo&units=Imperial
    City Number: 82 City_Name: sardarpur Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sardarpur&units=Imperial
    City Number: 83 City_Name: naze Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=naze&units=Imperial
    City Number: 84 City_Name: tura Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tura&units=Imperial
    City Number: 85 City_Name: saint-joseph Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saint-joseph&units=Imperial
    City Number: 86 City_Name: kavieng Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kavieng&units=Imperial
    City Number: 87 City_Name: barrow Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=barrow&units=Imperial
    City Number: 88 City_Name: kroya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kroya&units=Imperial
    City Number: 89 City_Name: longyearbyen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=longyearbyen&units=Imperial
    City Number: 90 City_Name: batagay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=batagay&units=Imperial
    City Number: 91 City_Name: airai Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=airai&units=Imperial
    City Number: 92 City_Name: mar del plata Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mar del plata&units=Imperial
    City Number: 93 City_Name: baruun-urt Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=baruun-urt&units=Imperial
    City Number: 94 City_Name: dingle Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dingle&units=Imperial
    City Number: 95 City_Name: bredasdorp Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bredasdorp&units=Imperial
    City Number: 96 City_Name: hermanus Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hermanus&units=Imperial
    City Number: 97 City_Name: sur Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sur&units=Imperial
    City Number: 98 City_Name: pangnirtung Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pangnirtung&units=Imperial
    City Number: 99 City_Name: kuching Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kuching&units=Imperial
    City Number: 100 City_Name: bathsheba Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bathsheba&units=Imperial
    City Number: 101 City_Name: tual Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tual&units=Imperial
    City Number: 102 City_Name: thompson Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=thompson&units=Imperial
    City Number: 103 City_Name: bluff Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bluff&units=Imperial
    City Number: 104 City_Name: praia da vitoria Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=praia da vitoria&units=Imperial
    City Number: 105 City_Name: saint anthony Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saint anthony&units=Imperial
    City Number: 106 City_Name: taoudenni Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=taoudenni&units=Imperial
    City Number: 107 City_Name: oktyabrskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=oktyabrskiy&units=Imperial
    City Number: 108 City_Name: tchibanga Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tchibanga&units=Imperial
    City Number: 109 City_Name: yulara Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yulara&units=Imperial
    City Number: 110 City_Name: shimsk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=shimsk&units=Imperial
    City Number: 111 City_Name: tuatapere Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tuatapere&units=Imperial
    City Number: 112 City_Name: kichera Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kichera&units=Imperial
    City Number: 113 City_Name: atasu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=atasu&units=Imperial
    City Number: 114 City_Name: george Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=george&units=Imperial
    City Number: 115 City_Name: codrington Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=codrington&units=Imperial
    City Number: 116 City_Name: clyde river Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=clyde river&units=Imperial
    City Number: 117 City_Name: betare oya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=betare oya&units=Imperial
    City Number: 118 City_Name: tuktoyaktuk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tuktoyaktuk&units=Imperial
    City Number: 119 City_Name: pacific grove Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pacific grove&units=Imperial
    City Number: 120 City_Name: hithadhoo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hithadhoo&units=Imperial
    City Number: 121 City_Name: saint-philippe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saint-philippe&units=Imperial
    City Number: 122 City_Name: cocoa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cocoa&units=Imperial
    City Number: 123 City_Name: tornio Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tornio&units=Imperial
    City Number: 124 City_Name: esperance Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=esperance&units=Imperial
    City Number: 125 City_Name: carnarvon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=carnarvon&units=Imperial
    City Number: 126 City_Name: hambantota Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hambantota&units=Imperial
    City Number: 127 City_Name: padang Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=padang&units=Imperial
    City Number: 128 City_Name: kodiak Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kodiak&units=Imperial
    City Number: 129 City_Name: castro Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=castro&units=Imperial
    City Number: 130 City_Name: shakawe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=shakawe&units=Imperial
    City Number: 131 City_Name: gazli Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=gazli&units=Imperial
    City Number: 132 City_Name: bangassou Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bangassou&units=Imperial
    City Number: 133 City_Name: klaksvik Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=klaksvik&units=Imperial
    City Number: 134 City_Name: yarensk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yarensk&units=Imperial
    City Number: 135 City_Name: bambous virieux Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bambous virieux&units=Imperial
    City Number: 136 City_Name: kavaratti Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kavaratti&units=Imperial
    City Number: 137 City_Name: tiksi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tiksi&units=Imperial
    City Number: 138 City_Name: comodoro rivadavia Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=comodoro rivadavia&units=Imperial
    City Number: 139 City_Name: lagoa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lagoa&units=Imperial
    City Number: 140 City_Name: moose factory Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=moose factory&units=Imperial
    City Number: 141 City_Name: norman wells Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=norman wells&units=Imperial
    City Number: 142 City_Name: cayenne Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cayenne&units=Imperial
    City Number: 143 City_Name: kabalo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kabalo&units=Imperial
    City Number: 144 City_Name: samoylovka Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=samoylovka&units=Imperial
    City Number: 145 City_Name: hualmay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hualmay&units=Imperial
    City Number: 146 City_Name: east london Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=east london&units=Imperial
    City Number: 147 City_Name: upernavik Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=upernavik&units=Imperial
    City Number: 148 City_Name: neryungri Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=neryungri&units=Imperial
    City Number: 149 City_Name: jamestown Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=jamestown&units=Imperial
    City Number: 150 City_Name: muswellbrook Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=muswellbrook&units=Imperial
    City Number: 151 City_Name: san ramon de la nueva oran Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san ramon de la nueva oran&units=Imperial
    City Number: 152 City_Name: poum Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=poum&units=Imperial
    City Number: 153 City_Name: teguldet Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=teguldet&units=Imperial
    City Number: 154 City_Name: lorengau Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lorengau&units=Imperial
    City Number: 155 City_Name: cabedelo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cabedelo&units=Imperial
    City Number: 156 City_Name: vila velha Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vila velha&units=Imperial
    City Number: 157 City_Name: tyumentsevo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tyumentsevo&units=Imperial
    City Number: 158 City_Name: novoasbest Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=novoasbest&units=Imperial
    City Number: 159 City_Name: skibbereen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=skibbereen&units=Imperial
    City Number: 160 City_Name: batemans bay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=batemans bay&units=Imperial
    City Number: 161 City_Name: sayyan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sayyan&units=Imperial
    City Number: 162 City_Name: asosa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=asosa&units=Imperial
    City Number: 163 City_Name: san juan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san juan&units=Imperial
    City Number: 164 City_Name: chuy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=chuy&units=Imperial
    City Number: 165 City_Name: saint-francois Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saint-francois&units=Imperial
    City Number: 166 City_Name: deputatskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=deputatskiy&units=Imperial
    City Number: 167 City_Name: sokoni Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sokoni&units=Imperial
    City Number: 168 City_Name: bushehr Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bushehr&units=Imperial
    City Number: 169 City_Name: garowe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=garowe&units=Imperial
    City Number: 170 City_Name: saskylakh Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saskylakh&units=Imperial
    City Number: 171 City_Name: port hedland Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port hedland&units=Imperial
    City Number: 172 City_Name: aguimes Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aguimes&units=Imperial
    City Number: 173 City_Name: stepnyak Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=stepnyak&units=Imperial
    City Number: 174 City_Name: pevek Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pevek&units=Imperial
    City Number: 175 City_Name: new norfolk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=new norfolk&units=Imperial
    City Number: 176 City_Name: pedreiras Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pedreiras&units=Imperial
    City Number: 177 City_Name: sterling Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sterling&units=Imperial
    City Number: 178 City_Name: nouadhibou Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nouadhibou&units=Imperial
    City Number: 179 City_Name: panguna Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=panguna&units=Imperial
    City Number: 180 City_Name: kisangani Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kisangani&units=Imperial
    City Number: 181 City_Name: kavarna Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kavarna&units=Imperial
    City Number: 182 City_Name: conde Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=conde&units=Imperial
    City Number: 183 City_Name: iqaluit Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=iqaluit&units=Imperial
    City Number: 184 City_Name: hilo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hilo&units=Imperial
    City Number: 185 City_Name: saldanha Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saldanha&units=Imperial
    City Number: 186 City_Name: betafo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=betafo&units=Imperial
    City Number: 187 City_Name: belmonte Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=belmonte&units=Imperial
    City Number: 188 City_Name: faanui Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=faanui&units=Imperial
    City Number: 189 City_Name: ambon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ambon&units=Imperial
    City Number: 190 City_Name: pisco Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pisco&units=Imperial
    City Number: 191 City_Name: husavik Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=husavik&units=Imperial
    City Number: 192 City_Name: sujangarh Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sujangarh&units=Imperial
    City Number: 193 City_Name: lavrentiya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lavrentiya&units=Imperial
    City Number: 194 City_Name: lormi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lormi&units=Imperial
    City Number: 195 City_Name: atar Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=atar&units=Imperial
    City Number: 196 City_Name: hilton head island Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hilton head island&units=Imperial
    City Number: 197 City_Name: vawkavysk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vawkavysk&units=Imperial
    City Number: 198 City_Name: lata Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lata&units=Imperial
    City Number: 199 City_Name: bubaque Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bubaque&units=Imperial
    City Number: 200 City_Name: palmer Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=palmer&units=Imperial
    City Number: 201 City_Name: port-gentil Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port-gentil&units=Imperial
    City Number: 202 City_Name: saint george Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saint george&units=Imperial
    City Number: 203 City_Name: beringovskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=beringovskiy&units=Imperial
    City Number: 204 City_Name: cabra Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cabra&units=Imperial
    City Number: 205 City_Name: paamiut Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=paamiut&units=Imperial
    City Number: 206 City_Name: hanyang Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hanyang&units=Imperial
    City Number: 207 City_Name: aracati Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aracati&units=Imperial
    City Number: 208 City_Name: narsaq Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=narsaq&units=Imperial
    City Number: 209 City_Name: kumylzhenskaya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kumylzhenskaya&units=Imperial
    City Number: 210 City_Name: milkovo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=milkovo&units=Imperial
    City Number: 211 City_Name: tucumcari Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tucumcari&units=Imperial
    City Number: 212 City_Name: portales Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=portales&units=Imperial
    City Number: 213 City_Name: hinatuan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hinatuan&units=Imperial
    City Number: 214 City_Name: sorland Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sorland&units=Imperial
    City Number: 215 City_Name: mastic beach Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mastic beach&units=Imperial
    City Number: 216 City_Name: victoria Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=victoria&units=Imperial
    City Number: 217 City_Name: kimbe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kimbe&units=Imperial
    City Number: 218 City_Name: santa vitoria do palmar Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=santa vitoria do palmar&units=Imperial
    City Number: 219 City_Name: gambela Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=gambela&units=Imperial
    City Number: 220 City_Name: ukiah Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ukiah&units=Imperial
    City Number: 221 City_Name: pitsunda Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pitsunda&units=Imperial
    City Number: 222 City_Name: dafeng Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dafeng&units=Imperial
    City Number: 223 City_Name: jinchang Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=jinchang&units=Imperial
    City Number: 224 City_Name: liancheng Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=liancheng&units=Imperial
    City Number: 225 City_Name: ust-kalmanka Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ust-kalmanka&units=Imperial
    City Number: 226 City_Name: rapid valley Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=rapid valley&units=Imperial
    City Number: 227 City_Name: koslan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=koslan&units=Imperial
    City Number: 228 City_Name: korcula Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=korcula&units=Imperial
    City Number: 229 City_Name: ormskirk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ormskirk&units=Imperial
    City Number: 230 City_Name: san joaquin Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san joaquin&units=Imperial
    City Number: 231 City_Name: goderich Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=goderich&units=Imperial
    City Number: 232 City_Name: nikolayevsk-na-amure Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nikolayevsk-na-amure&units=Imperial
    City Number: 233 City_Name: markova Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=markova&units=Imperial
    City Number: 234 City_Name: lufilufi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lufilufi&units=Imperial
    City Number: 235 City_Name: ratnagiri Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ratnagiri&units=Imperial
    City Number: 236 City_Name: cherskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cherskiy&units=Imperial
    City Number: 237 City_Name: indramayu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=indramayu&units=Imperial
    City Number: 238 City_Name: ettenheim Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ettenheim&units=Imperial
    City Number: 239 City_Name: salaga Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=salaga&units=Imperial
    City Number: 240 City_Name: saltillo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saltillo&units=Imperial
    City Number: 241 City_Name: katsuura Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=katsuura&units=Imperial
    City Number: 242 City_Name: boa vista Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=boa vista&units=Imperial
    City Number: 243 City_Name: zhangye Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zhangye&units=Imperial
    City Number: 244 City_Name: souillac Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=souillac&units=Imperial
    City Number: 245 City_Name: itambacuri Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=itambacuri&units=Imperial
    City Number: 246 City_Name: tandlianwala Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tandlianwala&units=Imperial
    City Number: 247 City_Name: port elizabeth Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port elizabeth&units=Imperial
    City Number: 248 City_Name: ostrovnoy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ostrovnoy&units=Imperial
    City Number: 249 City_Name: chokurdakh Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=chokurdakh&units=Imperial
    City Number: 250 City_Name: nikolskoye Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nikolskoye&units=Imperial
    City Number: 251 City_Name: aquiraz Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aquiraz&units=Imperial
    City Number: 252 City_Name: volot Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=volot&units=Imperial
    City Number: 253 City_Name: manthani Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=manthani&units=Imperial
    City Number: 254 City_Name: omsukchan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=omsukchan&units=Imperial
    City Number: 255 City_Name: port keats Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port keats&units=Imperial
    City Number: 256 City_Name: acapulco Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=acapulco&units=Imperial
    City Number: 257 City_Name: aklavik Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aklavik&units=Imperial
    City Number: 258 City_Name: fare Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=fare&units=Imperial
    City Number: 259 City_Name: dingwall Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dingwall&units=Imperial
    City Number: 260 City_Name: adre Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=adre&units=Imperial
    City Number: 261 City_Name: ende Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ende&units=Imperial
    City Number: 262 City_Name: forest grove Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=forest grove&units=Imperial
    City Number: 263 City_Name: tsumeb Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tsumeb&units=Imperial
    City Number: 264 City_Name: ilulissat Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ilulissat&units=Imperial
    City Number: 265 City_Name: shenjiamen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=shenjiamen&units=Imperial
    City Number: 266 City_Name: marataizes Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=marataizes&units=Imperial
    City Number: 267 City_Name: torbay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=torbay&units=Imperial
    City Number: 268 City_Name: bacolod Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bacolod&units=Imperial
    City Number: 269 City_Name: nacala Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nacala&units=Imperial
    City Number: 270 City_Name: constantine Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=constantine&units=Imperial
    City Number: 271 City_Name: santa isabel Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=santa isabel&units=Imperial
    City Number: 272 City_Name: gravdal Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=gravdal&units=Imperial
    City Number: 273 City_Name: zaraza Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zaraza&units=Imperial
    City Number: 274 City_Name: charters towers Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=charters towers&units=Imperial
    City Number: 275 City_Name: martapura Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=martapura&units=Imperial
    City Number: 276 City_Name: misratah Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=misratah&units=Imperial
    City Number: 277 City_Name: canico Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=canico&units=Imperial
    City Number: 278 City_Name: geraldton Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=geraldton&units=Imperial
    City Number: 279 City_Name: gizo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=gizo&units=Imperial
    City Number: 280 City_Name: banjar Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=banjar&units=Imperial
    City Number: 281 City_Name: amos Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=amos&units=Imperial
    City Number: 282 City_Name: port hardy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port hardy&units=Imperial
    City Number: 283 City_Name: mount gambier Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mount gambier&units=Imperial
    City Number: 284 City_Name: navahrudak Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=navahrudak&units=Imperial
    City Number: 285 City_Name: yerbogachen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yerbogachen&units=Imperial
    City Number: 286 City_Name: cabo san lucas Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cabo san lucas&units=Imperial
    City Number: 287 City_Name: arlit Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=arlit&units=Imperial
    City Number: 288 City_Name: san roque Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san roque&units=Imperial
    City Number: 289 City_Name: margate Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=margate&units=Imperial
    City Number: 290 City_Name: jermuk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=jermuk&units=Imperial
    City Number: 291 City_Name: los llanos de aridane Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=los llanos de aridane&units=Imperial
    City Number: 292 City_Name: magadan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=magadan&units=Imperial
    City Number: 293 City_Name: saint-pierre Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=saint-pierre&units=Imperial
    City Number: 294 City_Name: leeton Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=leeton&units=Imperial
    City Number: 295 City_Name: manokwari Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=manokwari&units=Imperial
    City Number: 296 City_Name: lanciano Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lanciano&units=Imperial
    City Number: 297 City_Name: provideniya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=provideniya&units=Imperial
    City Number: 298 City_Name: guerrero negro Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=guerrero negro&units=Imperial
    City Number: 299 City_Name: tubmanburg Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tubmanburg&units=Imperial
    City Number: 300 City_Name: ariquemes Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ariquemes&units=Imperial
    City Number: 301 City_Name: karpogory Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=karpogory&units=Imperial
    City Number: 302 City_Name: qasigiannguit Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=qasigiannguit&units=Imperial
    City Number: 303 City_Name: arman Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=arman&units=Imperial
    City Number: 304 City_Name: contratacion Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=contratacion&units=Imperial
    City Number: 305 City_Name: port blair Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=port blair&units=Imperial
    City Number: 306 City_Name: tilichiki Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tilichiki&units=Imperial
    City Number: 307 City_Name: wladyslawowo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=wladyslawowo&units=Imperial
    City Number: 308 City_Name: bilma Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=bilma&units=Imperial
    City Number: 309 City_Name: morondava Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=morondava&units=Imperial
    City Number: 310 City_Name: montanha Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=montanha&units=Imperial
    City Number: 311 City_Name: zhigansk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zhigansk&units=Imperial
    City Number: 312 City_Name: sabha Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sabha&units=Imperial
    City Number: 313 City_Name: sorong Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sorong&units=Imperial
    City Number: 314 City_Name: mackay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mackay&units=Imperial
    City Number: 315 City_Name: keuruu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=keuruu&units=Imperial
    City Number: 316 City_Name: huarmey Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=huarmey&units=Imperial
    City Number: 317 City_Name: muzhi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=muzhi&units=Imperial
    City Number: 318 City_Name: marzuq Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=marzuq&units=Imperial
    City Number: 319 City_Name: aasiaat Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aasiaat&units=Imperial
    City Number: 320 City_Name: gamboula Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=gamboula&units=Imperial
    City Number: 321 City_Name: kathmandu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kathmandu&units=Imperial
    City Number: 322 City_Name: beloha Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=beloha&units=Imperial
    City Number: 323 City_Name: san angelo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san angelo&units=Imperial
    City Number: 324 City_Name: haines junction Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=haines junction&units=Imperial
    City Number: 325 City_Name: calarasi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=calarasi&units=Imperial
    City Number: 326 City_Name: tagusao Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tagusao&units=Imperial
    City Number: 327 City_Name: dumas Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dumas&units=Imperial
    City Number: 328 City_Name: hami Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hami&units=Imperial
    City Number: 329 City_Name: yanam Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yanam&units=Imperial
    City Number: 330 City_Name: lasa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lasa&units=Imperial
    City Number: 331 City_Name: durango Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=durango&units=Imperial
    City Number: 332 City_Name: dunedin Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dunedin&units=Imperial
    City Number: 333 City_Name: kastamonu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kastamonu&units=Imperial
    City Number: 334 City_Name: namibe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=namibe&units=Imperial
    City Number: 335 City_Name: kalawit Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kalawit&units=Imperial
    City Number: 336 City_Name: yumen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yumen&units=Imperial
    City Number: 337 City_Name: guilin Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=guilin&units=Imperial
    City Number: 338 City_Name: roros Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=roros&units=Imperial
    City Number: 339 City_Name: veraval Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=veraval&units=Imperial
    City Number: 340 City_Name: northam Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=northam&units=Imperial
    City Number: 341 City_Name: swan hill Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=swan hill&units=Imperial
    City Number: 342 City_Name: ahlat Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ahlat&units=Imperial
    City Number: 343 City_Name: waipawa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=waipawa&units=Imperial
    City Number: 344 City_Name: zhumadian Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zhumadian&units=Imperial
    City Number: 345 City_Name: chute-aux-outardes Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=chute-aux-outardes&units=Imperial
    City Number: 346 City_Name: richards bay Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=richards bay&units=Imperial
    City Number: 347 City_Name: barkhan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=barkhan&units=Imperial
    City Number: 348 City_Name: outjo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=outjo&units=Imperial
    City Number: 349 City_Name: baran Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=baran&units=Imperial
    City Number: 350 City_Name: toguchin Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=toguchin&units=Imperial
    City Number: 351 City_Name: dawlatabad Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dawlatabad&units=Imperial
    City Number: 352 City_Name: aleksandrovsk-sakhalinskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aleksandrovsk-sakhalinskiy&units=Imperial
    City Number: 353 City_Name: gobabis Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=gobabis&units=Imperial
    City Number: 354 City_Name: quatre cocos Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=quatre cocos&units=Imperial
    City Number: 355 City_Name: marienburg Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=marienburg&units=Imperial
    City Number: 356 City_Name: udachnyy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=udachnyy&units=Imperial
    City Number: 357 City_Name: cockburn town Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=cockburn town&units=Imperial
    City Number: 358 City_Name: hamilton Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hamilton&units=Imperial
    City Number: 359 City_Name: mercedes Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mercedes&units=Imperial
    City Number: 360 City_Name: pemba Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pemba&units=Imperial
    City Number: 361 City_Name: wajir Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=wajir&units=Imperial
    City Number: 362 City_Name: sujiatun Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sujiatun&units=Imperial
    City Number: 363 City_Name: portland Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=portland&units=Imperial
    City Number: 364 City_Name: beisfjord Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=beisfjord&units=Imperial
    City Number: 365 City_Name: venustiano carranza Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=venustiano carranza&units=Imperial
    City Number: 366 City_Name: auki Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=auki&units=Imperial
    City Number: 367 City_Name: marfino Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=marfino&units=Imperial
    City Number: 368 City_Name: yeppoon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=yeppoon&units=Imperial
    City Number: 369 City_Name: inverell Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=inverell&units=Imperial
    City Number: 370 City_Name: luena Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=luena&units=Imperial
    City Number: 371 City_Name: turgenevo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=turgenevo&units=Imperial
    City Number: 372 City_Name: arroyo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=arroyo&units=Imperial
    City Number: 373 City_Name: sibolga Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sibolga&units=Imperial
    City Number: 374 City_Name: brae Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=brae&units=Imperial
    City Number: 375 City_Name: savadisla Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=savadisla&units=Imperial
    City Number: 376 City_Name: agarak Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=agarak&units=Imperial
    City Number: 377 City_Name: amapa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=amapa&units=Imperial
    City Number: 378 City_Name: grand gaube Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=grand gaube&units=Imperial
    City Number: 379 City_Name: viedma Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=viedma&units=Imperial
    City Number: 380 City_Name: orocue Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=orocue&units=Imperial
    City Number: 381 City_Name: vao Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vao&units=Imperial
    City Number: 382 City_Name: faya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=faya&units=Imperial
    City Number: 383 City_Name: alyangula Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=alyangula&units=Imperial
    City Number: 384 City_Name: okhotsk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=okhotsk&units=Imperial
    City Number: 385 City_Name: baoding Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=baoding&units=Imperial
    City Number: 386 City_Name: diapaga Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=diapaga&units=Imperial
    City Number: 387 City_Name: governador valadares Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=governador valadares&units=Imperial
    City Number: 388 City_Name: seddon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=seddon&units=Imperial
    City Number: 389 City_Name: lexington Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=lexington&units=Imperial
    City Number: 390 City_Name: nchelenge Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nchelenge&units=Imperial
    City Number: 391 City_Name: kaitangata Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kaitangata&units=Imperial
    City Number: 392 City_Name: labuhan Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=labuhan&units=Imperial
    City Number: 393 City_Name: kontagora Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kontagora&units=Imperial
    City Number: 394 City_Name: hobyo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hobyo&units=Imperial
    City Number: 395 City_Name: tiznit Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tiznit&units=Imperial
    City Number: 396 City_Name: alice town Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=alice town&units=Imperial
    City Number: 397 City_Name: kamenka Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kamenka&units=Imperial
    City Number: 398 City_Name: puerto escondido Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=puerto escondido&units=Imperial
    City Number: 399 City_Name: salalah Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=salalah&units=Imperial
    City Number: 400 City_Name: moerai Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=moerai&units=Imperial
    City Number: 401 City_Name: seoul Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=seoul&units=Imperial
    City Number: 402 City_Name: boguchany Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=boguchany&units=Imperial
    City Number: 403 City_Name: ossora Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ossora&units=Imperial
    City Number: 404 City_Name: najran Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=najran&units=Imperial
    City Number: 405 City_Name: ulladulla Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ulladulla&units=Imperial
    City Number: 406 City_Name: dalvik Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=dalvik&units=Imperial
    City Number: 407 City_Name: manga Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=manga&units=Imperial
    City Number: 408 City_Name: grenada Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=grenada&units=Imperial
    City Number: 409 City_Name: ponta do sol Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ponta do sol&units=Imperial
    City Number: 410 City_Name: solnechnyy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=solnechnyy&units=Imperial
    City Number: 411 City_Name: pozo colorado Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pozo colorado&units=Imperial
    City Number: 412 City_Name: tandalti Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tandalti&units=Imperial
    City Number: 413 City_Name: san patricio Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san patricio&units=Imperial
    City Number: 414 City_Name: zyryanka Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zyryanka&units=Imperial
    City Number: 415 City_Name: chegutu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=chegutu&units=Imperial
    City Number: 416 City_Name: srednekolymsk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=srednekolymsk&units=Imperial
    City Number: 417 City_Name: constitucion Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=constitucion&units=Imperial
    City Number: 418 City_Name: jalu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=jalu&units=Imperial
    City Number: 419 City_Name: zharkent Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zharkent&units=Imperial
    City Number: 420 City_Name: laon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=laon&units=Imperial
    City Number: 421 City_Name: murighiol Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=murighiol&units=Imperial
    City Number: 422 City_Name: svetlaya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=svetlaya&units=Imperial
    City Number: 423 City_Name: genhe Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=genhe&units=Imperial
    City Number: 424 City_Name: kanigoro Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kanigoro&units=Imperial
    City Number: 425 City_Name: great falls Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=great falls&units=Imperial
    City Number: 426 City_Name: horsham Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=horsham&units=Imperial
    City Number: 427 City_Name: porto velho Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=porto velho&units=Imperial
    City Number: 428 City_Name: punta de bombon Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=punta de bombon&units=Imperial
    City Number: 429 City_Name: ust-nera Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ust-nera&units=Imperial
    City Number: 430 City_Name: raudeberg Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=raudeberg&units=Imperial
    City Number: 431 City_Name: madaoua Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=madaoua&units=Imperial
    City Number: 432 City_Name: necochea Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=necochea&units=Imperial
    City Number: 433 City_Name: artesia Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=artesia&units=Imperial
    City Number: 434 City_Name: pontal do parana Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pontal do parana&units=Imperial
    City Number: 435 City_Name: vestmannaeyjar Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=vestmannaeyjar&units=Imperial
    City Number: 436 City_Name: komsomolskiy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=komsomolskiy&units=Imperial
    City Number: 437 City_Name: alofi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=alofi&units=Imperial
    City Number: 438 City_Name: ruwi Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ruwi&units=Imperial
    City Number: 439 City_Name: namwala Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=namwala&units=Imperial
    City Number: 440 City_Name: popondetta Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=popondetta&units=Imperial
    City Number: 441 City_Name: barao de melgaco Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=barao de melgaco&units=Imperial
    City Number: 442 City_Name: riyadh Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=riyadh&units=Imperial
    City Number: 443 City_Name: reading Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=reading&units=Imperial
    City Number: 444 City_Name: sao joao da barra Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sao joao da barra&units=Imperial
    City Number: 445 City_Name: atherton Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=atherton&units=Imperial
    City Number: 446 City_Name: opuwo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=opuwo&units=Imperial
    City Number: 447 City_Name: minab Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=minab&units=Imperial
    City Number: 448 City_Name: iguape Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=iguape&units=Imperial
    City Number: 449 City_Name: novoagansk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=novoagansk&units=Imperial
    City Number: 450 City_Name: george town Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=george town&units=Imperial
    City Number: 451 City_Name: road town Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=road town&units=Imperial
    City Number: 452 City_Name: snezhnogorsk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=snezhnogorsk&units=Imperial
    City Number: 453 City_Name: buenos aires Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=buenos aires&units=Imperial
    City Number: 454 City_Name: winslow Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=winslow&units=Imperial
    City Number: 455 City_Name: sovkhoznyy Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=sovkhoznyy&units=Imperial
    City Number: 456 City_Name: ahuimanu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ahuimanu&units=Imperial
    City Number: 457 City_Name: hays Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=hays&units=Imperial
    City Number: 458 City_Name: la romana Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=la romana&units=Imperial
    City Number: 459 City_Name: mandal Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mandal&units=Imperial
    City Number: 460 City_Name: broome Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=broome&units=Imperial
    City Number: 461 City_Name: avera Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=avera&units=Imperial
    City Number: 462 City_Name: nemencine Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nemencine&units=Imperial
    City Number: 463 City_Name: nuuk Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nuuk&units=Imperial
    City Number: 464 City_Name: la ronge Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=la ronge&units=Imperial
    City Number: 465 City_Name: kizema Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kizema&units=Imperial
    City Number: 466 City_Name: nara Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=nara&units=Imperial
    City Number: 467 City_Name: la palma Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=la palma&units=Imperial
    City Number: 468 City_Name: san jeronimo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=san jeronimo&units=Imperial
    City Number: 469 City_Name: pochutla Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=pochutla&units=Imperial
    City Number: 470 City_Name: khandbari Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=khandbari&units=Imperial
    City Number: 471 City_Name: xapuri Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=xapuri&units=Imperial
    City Number: 472 City_Name: kirakira Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kirakira&units=Imperial
    City Number: 473 City_Name: chico Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=chico&units=Imperial
    City Number: 474 City_Name: laguna Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=laguna&units=Imperial
    City Number: 475 City_Name: mareeba Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mareeba&units=Imperial
    City Number: 476 City_Name: ilabaya Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ilabaya&units=Imperial
    City Number: 477 City_Name: college Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=college&units=Imperial
    City Number: 478 City_Name: santander Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=santander&units=Imperial
    City Number: 479 City_Name: todos santos Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=todos santos&units=Imperial
    City Number: 480 City_Name: coahuayana Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=coahuayana&units=Imperial
    City Number: 481 City_Name: brigantine Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=brigantine&units=Imperial
    City Number: 482 City_Name: naduvattam Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=naduvattam&units=Imperial
    City Number: 483 City_Name: staryy nadym Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=staryy nadym&units=Imperial
    City Number: 484 City_Name: zhanaozen Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=zhanaozen&units=Imperial
    City Number: 485 City_Name: aktau Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=aktau&units=Imperial
    City Number: 486 City_Name: valentin gomez farias Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=valentin gomez farias&units=Imperial
    City Number: 487 City_Name: kuji Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kuji&units=Imperial
    City Number: 488 City_Name: chicama Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=chicama&units=Imperial
    City Number: 489 City_Name: ahipara Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ahipara&units=Imperial
    City Number: 490 City_Name: ibague Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ibague&units=Imperial
    City Number: 491 City_Name: santo antonio do monte Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=santo antonio do monte&units=Imperial
    City Number: 492 City_Name: mgandu Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=mgandu&units=Imperial
    City Number: 493 City_Name: ancud Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ancud&units=Imperial
    City Number: 494 City_Name: deder Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=deder&units=Imperial
    City Number: 495 City_Name: acajutla Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=acajutla&units=Imperial
    City Number: 496 City_Name: tripoli Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=tripoli&units=Imperial
    City Number: 497 City_Name: ixtapa Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ixtapa&units=Imperial
    City Number: 498 City_Name: ust-kulom Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=ust-kulom&units=Imperial
    City Number: 499 City_Name: kudahuvadhoo Query_URL: http://api.openweathermap.org/data/2.5/weather?appid=e2951494bae8033d90e5cc8417add725&q=kudahuvadhoo&units=Imperial
    500
    


```python
write_to_csv = weatherDF.to_csv('Assignment6.csv',sep = ',')
cities
```




    ['rikitea',
     'hobart',
     'kaduqli',
     'cairns',
     'tezu',
     'avarua',
     'butaritari',
     'neuquen',
     'ushuaia',
     'kapaa',
     'severo-kurilsk',
     'bilibino',
     'teya',
     'ouesso',
     'port alfred',
     'santa maria',
     'salinopolis',
     'vardo',
     'punta arenas',
     'mataura',
     'aswan',
     'kahului',
     'nome',
     'vila franca do campo',
     'tasiilaq',
     'khatanga',
     'ribeira grande',
     'sao filipe',
     'cidreira',
     'bassar',
     'halifax',
     'bethel',
     'lazaro cardenas',
     'harper',
     'atuona',
     'coquimbo',
     'leningradskiy',
     'arraial do cabo',
     'lebu',
     'pangody',
     'bismarck',
     'vestmanna',
     'qaanaaq',
     'nakhon thai',
     'lamas',
     'port lincoln',
     'shaunavon',
     'luderitz',
     'albany',
     'cape town',
     'baykit',
     'yellowknife',
     'kruisfontein',
     'quelimane',
     'fortuna',
     'touros',
     'talnakh',
     'makakilo city',
     'lompoc',
     'anadyr',
     'krathum baen',
     'broken hill',
     'nhulunbuy',
     'sitka',
     'busselton',
     'vaini',
     'puerto ayora',
     'dzilam gonzalez',
     'lyaskelya',
     'storforshei',
     'jumla',
     'mahebourg',
     'dikson',
     'valdivia',
     'khani',
     'hasaki',
     'san cristobal',
     'nelson bay',
     'georgetown',
     'atocha',
     'masakin',
     'barsovo',
     'sardarpur',
     'naze',
     'tura',
     'saint-joseph',
     'kavieng',
     'barrow',
     'kroya',
     'longyearbyen',
     'batagay',
     'airai',
     'mar del plata',
     'baruun-urt',
     'dingle',
     'bredasdorp',
     'hermanus',
     'sur',
     'pangnirtung',
     'kuching',
     'bathsheba',
     'tual',
     'thompson',
     'bluff',
     'praia da vitoria',
     'saint anthony',
     'taoudenni',
     'oktyabrskiy',
     'tchibanga',
     'yulara',
     'shimsk',
     'tuatapere',
     'kichera',
     'atasu',
     'george',
     'codrington',
     'clyde river',
     'betare oya',
     'tuktoyaktuk',
     'pacific grove',
     'hithadhoo',
     'saint-philippe',
     'cocoa',
     'tornio',
     'esperance',
     'carnarvon',
     'hambantota',
     'padang',
     'kodiak',
     'castro',
     'shakawe',
     'gazli',
     'bangassou',
     'klaksvik',
     'yarensk',
     'bambous virieux',
     'kavaratti',
     'tiksi',
     'comodoro rivadavia',
     'lagoa',
     'moose factory',
     'norman wells',
     'cayenne',
     'kabalo',
     'samoylovka',
     'hualmay',
     'east london',
     'upernavik',
     'neryungri',
     'jamestown',
     'muswellbrook',
     'san ramon de la nueva oran',
     'poum',
     'teguldet',
     'lorengau',
     'cabedelo',
     'vila velha',
     'tyumentsevo',
     'novoasbest',
     'skibbereen',
     'batemans bay',
     'sayyan',
     'asosa',
     'san juan',
     'chuy',
     'saint-francois',
     'deputatskiy',
     'sokoni',
     'bushehr',
     'garowe',
     'saskylakh',
     'port hedland',
     'aguimes',
     'stepnyak',
     'pevek',
     'new norfolk',
     'pedreiras',
     'sterling',
     'nouadhibou',
     'panguna',
     'kisangani',
     'kavarna',
     'conde',
     'iqaluit',
     'hilo',
     'saldanha',
     'betafo',
     'belmonte',
     'faanui',
     'ambon',
     'pisco',
     'husavik',
     'sujangarh',
     'lavrentiya',
     'lormi',
     'atar',
     'hilton head island',
     'vawkavysk',
     'lata',
     'bubaque',
     'palmer',
     'port-gentil',
     'saint george',
     'beringovskiy',
     'cabra',
     'paamiut',
     'hanyang',
     'aracati',
     'narsaq',
     'kumylzhenskaya',
     'milkovo',
     'tucumcari',
     'portales',
     'hinatuan',
     'sorland',
     'mastic beach',
     'victoria',
     'kimbe',
     'santa vitoria do palmar',
     'gambela',
     'ukiah',
     'pitsunda',
     'dafeng',
     'jinchang',
     'liancheng',
     'ust-kalmanka',
     'rapid valley',
     'koslan',
     'korcula',
     'ormskirk',
     'san joaquin',
     'goderich',
     'nikolayevsk-na-amure',
     'markova',
     'lufilufi',
     'ratnagiri',
     'cherskiy',
     'indramayu',
     'ettenheim',
     'salaga',
     'saltillo',
     'katsuura',
     'boa vista',
     'zhangye',
     'souillac',
     'itambacuri',
     'tandlianwala',
     'port elizabeth',
     'ostrovnoy',
     'chokurdakh',
     'nikolskoye',
     'aquiraz',
     'volot',
     'manthani',
     'omsukchan',
     'port keats',
     'acapulco',
     'aklavik',
     'fare',
     'dingwall',
     'adre',
     'ende',
     'forest grove',
     'tsumeb',
     'ilulissat',
     'shenjiamen',
     'marataizes',
     'torbay',
     'bacolod',
     'nacala',
     'constantine',
     'santa isabel',
     'gravdal',
     'zaraza',
     'charters towers',
     'martapura',
     'misratah',
     'canico',
     'geraldton',
     'gizo',
     'banjar',
     'amos',
     'port hardy',
     'mount gambier',
     'navahrudak',
     'yerbogachen',
     'cabo san lucas',
     'arlit',
     'san roque',
     'margate',
     'jermuk',
     'los llanos de aridane',
     'magadan',
     'saint-pierre',
     'leeton',
     'manokwari',
     'lanciano',
     'provideniya',
     'guerrero negro',
     'tubmanburg',
     'ariquemes',
     'karpogory',
     'qasigiannguit',
     'arman',
     'contratacion',
     'port blair',
     'tilichiki',
     'wladyslawowo',
     'bilma',
     'morondava',
     'montanha',
     'zhigansk',
     'sabha',
     'sorong',
     'mackay',
     'keuruu',
     'huarmey',
     'muzhi',
     'marzuq',
     'aasiaat',
     'gamboula',
     'kathmandu',
     'beloha',
     'san angelo',
     'haines junction',
     'calarasi',
     'tagusao',
     'dumas',
     'hami',
     'yanam',
     'lasa',
     'durango',
     'dunedin',
     'kastamonu',
     'namibe',
     'kalawit',
     'yumen',
     'guilin',
     'roros',
     'veraval',
     'northam',
     'swan hill',
     'ahlat',
     'waipawa',
     'zhumadian',
     'chute-aux-outardes',
     'richards bay',
     'barkhan',
     'outjo',
     'baran',
     'toguchin',
     'dawlatabad',
     'aleksandrovsk-sakhalinskiy',
     'gobabis',
     'quatre cocos',
     'marienburg',
     'udachnyy',
     'cockburn town',
     'hamilton',
     'mercedes',
     'pemba',
     'wajir',
     'sujiatun',
     'portland',
     'beisfjord',
     'venustiano carranza',
     'auki',
     'marfino',
     'yeppoon',
     'inverell',
     'luena',
     'turgenevo',
     'arroyo',
     'sibolga',
     'brae',
     'savadisla',
     'agarak',
     'amapa',
     'grand gaube',
     'viedma',
     'orocue',
     'vao',
     'faya',
     'alyangula',
     'okhotsk',
     'baoding',
     'diapaga',
     'governador valadares',
     'seddon',
     'lexington',
     'nchelenge',
     'kaitangata',
     'labuhan',
     'kontagora',
     'hobyo',
     'tiznit',
     'alice town',
     'kamenka',
     'puerto escondido',
     'salalah',
     'moerai',
     'seoul',
     'boguchany',
     'ossora',
     'najran',
     'ulladulla',
     'dalvik',
     'manga',
     'grenada',
     'ponta do sol',
     'solnechnyy',
     'pozo colorado',
     'tandalti',
     'san patricio',
     'zyryanka',
     'chegutu',
     'srednekolymsk',
     'constitucion',
     'jalu',
     'zharkent',
     'laon',
     'murighiol',
     'svetlaya',
     'genhe',
     'kanigoro',
     'great falls',
     'horsham',
     'porto velho',
     'punta de bombon',
     'ust-nera',
     'raudeberg',
     'madaoua',
     'necochea',
     'artesia',
     'pontal do parana',
     'vestmannaeyjar',
     'komsomolskiy',
     'alofi',
     'ruwi',
     'namwala',
     'popondetta',
     'barao de melgaco',
     'riyadh',
     'reading',
     'sao joao da barra',
     'atherton',
     'opuwo',
     'minab',
     'iguape',
     'novoagansk',
     'george town',
     'road town',
     'snezhnogorsk',
     'buenos aires',
     'winslow',
     'sovkhoznyy',
     'ahuimanu',
     'hays',
     'la romana',
     'mandal',
     'broome',
     'avera',
     'nemencine',
     'nuuk',
     'la ronge',
     'kizema',
     'nara',
     'la palma',
     'san jeronimo',
     'pochutla',
     'khandbari',
     'xapuri',
     'kirakira',
     'chico',
     'laguna',
     'mareeba',
     'ilabaya',
     'college',
     'santander',
     'todos santos',
     'coahuayana',
     'brigantine',
     'naduvattam',
     'staryy nadym',
     'zhanaozen',
     'aktau',
     'valentin gomez farias',
     'kuji',
     'chicama',
     'ahipara',
     'ibague',
     'santo antonio do monte',
     'mgandu',
     'ancud',
     'deder',
     'acajutla',
     'tripoli',
     'ixtapa',
     'ust-kulom',
     'kudahuvadhoo']




```python
plt.scatter(weatherDF['Latitude'].apply(float), weatherDF['Temp'])

plt.title('Latitude vs. Temp')
plt.xlabel('Latitude')
plt.ylabel('Temp')
plt.show()
plt.savefig('Latitude vs. Temp.png')
```


![png](output_4_0.png)



```python

plt.scatter(weatherDF['Latitude'].apply(float), weatherDF['Humidity'])
plt.xlabel('Latitude')
plt.ylabel('Humidity')
plt.title('Latitude vs. Humidity')
plt.show()
plt.savefig('Latitude vs. Humidity.png')
```


![png](output_5_0.png)



```python
plt.scatter(weatherDF['Latitude'].apply(float), weatherDF['Cloudiness'])
plt.xlabel('Latitude')
plt.ylabel('Cloudiness')
plt.title('Latitude vs. Cloudiness')
plt.show()
plt.savefig('Latitude vs. Cloudiness.png')
```


![png](output_6_0.png)



```python
plt.scatter(weatherDF['Latitude'].apply(float), weatherDF['Wind Speed'])
plt.xlabel('Latitude')
plt.ylabel('Wind Speed')
plt.title('Latitude vs. Wind Speed')
plt.show()
plt.savefig('Latitude vs. Wind Speed.png')
```


![png](output_7_0.png)


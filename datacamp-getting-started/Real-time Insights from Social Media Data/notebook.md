
## 1. Local and global thought patterns
<p>While we might not be Twitter fans, we have to admit that it has a huge influence on the world (who doesn't know about Trump's tweets). Twitter data is not only gold in terms of insights, but <strong><em>Twitter-storms are available for analysis in near real-time</em></strong>. This means we can learn about the big waves of thoughts and moods around the world as they arise. </p>
<p>As any place filled with riches, Twitter has <em>security guards</em> blocking us from laying our hands on the data right away ⛔️ Some  authentication steps (really straightforward) are needed to call their APIs for data collection. Since our goal today is learning to extract insights from data, we have already gotten a green-pass from security ✅ Our data is ready for usage in the datasets folder — we can concentrate on the fun part! 🕵️‍♀️🌎
<br>
<br>
<img src="https://assets.datacamp.com/production/project_760/img/tweets_influence.png" style="width: 300px">
<hr>
<br>Twitter provides both global and local trends. Let's load and inspect data for topics that were hot worldwide (WW) and in the United States (US) at the moment of query  — snapshot of JSON response from the call to Twitter's <i>GET trends/place</i> API.</p>
<p><i><b>Note</b>: <a href="https://developer.twitter.com/en/docs/trends/trends-for-location/api-reference/get-trends-place.html">Here</a> is the documentation for this call, and <a href="https://developer.twitter.com/en/docs/api-reference-index.html">here</a> a full overview on Twitter's APIs.</i></p>

```python
# Loading json module
import json

# Load WW_trends and US_trends data into the the given variables respectively
WW_trends = json.loads(open('datasets/WWTrends.json').read())
US_trends = json.loads(open('datasets/USTrends.json').read())

# Inspecting data by printing out WW_trends and US_trends variables
print(WW_trends)
print(US_trends)
```

    [{'trends': [{'name': '#BeratKandili', 'url': 'http://twitter.com/search?q=%23BeratKandili', 'promoted_content': None, 'query': '%23BeratKandili', 'tweet_volume': 46373}, {'name': '#GoodFriday', 'url': 'http://twitter.com/search?q=%23GoodFriday', 'promoted_content': None, 'query': '%23GoodFriday', 'tweet_volume': 81891}, {'name': '#WeLoveTheEarth', 'url': 'http://twitter.com/search?q=%23WeLoveTheEarth', 'promoted_content': None, 'query': '%23WeLoveTheEarth', 'tweet_volume': 159698}, {'name': '#195TLdenTTVerilir', 'url': 'http://twitter.com/search?q=%23195TLdenTTVerilir', 'promoted_content': None, 'query': '%23195TLdenTTVerilir', 'tweet_volume': None}, {'name': '#AFLNorthDons', 'url': 'http://twitter.com/search?q=%23AFLNorthDons', 'promoted_content': None, 'query': '%23AFLNorthDons', 'tweet_volume': None}, {'name': 'Shiv Sena', 'url': 'http://twitter.com/search?q=%22Shiv+Sena%22', 'promoted_content': None, 'query': '%22Shiv+Sena%22', 'tweet_volume': None}, {'name': 'Lyra McKee', 'url': 'http://twitter.com/search?q=%22Lyra+McKee%22', 'promoted_content': None, 'query': '%22Lyra+McKee%22', 'tweet_volume': 17606}, {'name': 'Priyanka Chaturvedi', 'url': 'http://twitter.com/search?q=%22Priyanka+Chaturvedi%22', 'promoted_content': None, 'query': '%22Priyanka+Chaturvedi%22', 'tweet_volume': 22342}, {'name': 'Derry', 'url': 'http://twitter.com/search?q=Derry', 'promoted_content': None, 'query': 'Derry', 'tweet_volume': 28234}, {'name': '池袋の事故', 'url': 'http://twitter.com/search?q=%E6%B1%A0%E8%A2%8B%E3%81%AE%E4%BA%8B%E6%95%85', 'promoted_content': None, 'query': '%E6%B1%A0%E8%A2%8B%E3%81%AE%E4%BA%8B%E6%95%85', 'tweet_volume': 34381}, {'name': 'プリウス', 'url': 'http://twitter.com/search?q=%E3%83%97%E3%83%AA%E3%82%A6%E3%82%B9', 'promoted_content': None, 'query': '%E3%83%97%E3%83%AA%E3%82%A6%E3%82%B9', 'tweet_volume': 22944}, {'name': 'Hemant Karkare', 'url': 'http://twitter.com/search?q=%22Hemant+Karkare%22', 'promoted_content': None, 'query': '%22Hemant+Karkare%22', 'tweet_volume': 24067}, {'name': '高齢者', 'url': 'http://twitter.com/search?q=%E9%AB%98%E9%BD%A2%E8%80%85', 'promoted_content': None, 'query': '%E9%AB%98%E9%BD%A2%E8%80%85', 'tweet_volume': 28382}, {'name': '브이알', 'url': 'http://twitter.com/search?q=%EB%B8%8C%EC%9D%B4%EC%95%8C', 'promoted_content': None, 'query': '%EB%B8%8C%EC%9D%B4%EC%95%8C', 'tweet_volume': 15490}, {'name': '刀ステ', 'url': 'http://twitter.com/search?q=%E5%88%80%E3%82%B9%E3%83%86', 'promoted_content': None, 'query': '%E5%88%80%E3%82%B9%E3%83%86', 'tweet_volume': None}, {'name': '免許返納', 'url': 'http://twitter.com/search?q=%E5%85%8D%E8%A8%B1%E8%BF%94%E7%B4%8D', 'promoted_content': None, 'query': '%E5%85%8D%E8%A8%B1%E8%BF%94%E7%B4%8D', 'tweet_volume': None}, {'name': 'Berat Kandilimiz', 'url': 'http://twitter.com/search?q=%22Berat+Kandilimiz%22', 'promoted_content': None, 'query': '%22Berat+Kandilimiz%22', 'tweet_volume': 10901}, {'name': 'örgütdeğil arkadaşgrubu', 'url': 'http://twitter.com/search?q=%22%C3%B6rg%C3%BCtde%C4%9Fil+arkada%C5%9Fgrubu%22', 'promoted_content': None, 'query': '%22%C3%B6rg%C3%BCtde%C4%9Fil+arkada%C5%9Fgrubu%22', 'tweet_volume': None}, {'name': 'グレア', 'url': 'http://twitter.com/search?q=%E3%82%B0%E3%83%AC%E3%82%A2', 'promoted_content': None, 'query': '%E3%82%B0%E3%83%AC%E3%82%A2', 'tweet_volume': 23485}, {'name': '東京・池袋衝突事故', 'url': 'http://twitter.com/search?q=%E6%9D%B1%E4%BA%AC%E3%83%BB%E6%B1%A0%E8%A2%8B%E8%A1%9D%E7%AA%81%E4%BA%8B%E6%95%85', 'promoted_content': None, 'query': '%E6%9D%B1%E4%BA%AC%E3%83%BB%E6%B1%A0%E8%A2%8B%E8%A1%9D%E7%AA%81%E4%BA%8B%E6%95%85', 'tweet_volume': None}, {'name': '重体の女性と女児', 'url': 'http://twitter.com/search?q=%E9%87%8D%E4%BD%93%E3%81%AE%E5%A5%B3%E6%80%A7%E3%81%A8%E5%A5%B3%E5%85%90', 'promoted_content': None, 'query': '%E9%87%8D%E4%BD%93%E3%81%AE%E5%A5%B3%E6%80%A7%E3%81%A8%E5%A5%B3%E5%85%90', 'tweet_volume': None}, {'name': 'Lil Dicky', 'url': 'http://twitter.com/search?q=%22Lil+Dicky%22', 'promoted_content': None, 'query': '%22Lil+Dicky%22', 'tweet_volume': 42461}, {'name': '歩行者', 'url': 'http://twitter.com/search?q=%E6%AD%A9%E8%A1%8C%E8%80%85', 'promoted_content': None, 'query': '%E6%AD%A9%E8%A1%8C%E8%80%85', 'tweet_volume': 25405}, {'name': 'Derrick White', 'url': 'http://twitter.com/search?q=%22Derrick+White%22', 'promoted_content': None, 'query': '%22Derrick+White%22', 'tweet_volume': 27104}, {'name': '十二国記', 'url': 'http://twitter.com/search?q=%E5%8D%81%E4%BA%8C%E5%9B%BD%E8%A8%98', 'promoted_content': None, 'query': '%E5%8D%81%E4%BA%8C%E5%9B%BD%E8%A8%98', 'tweet_volume': 46803}, {'name': '#KpuJanganCurang', 'url': 'http://twitter.com/search?q=%23KpuJanganCurang', 'promoted_content': None, 'query': '%23KpuJanganCurang', 'tweet_volume': 75384}, {'name': '#HayırlıCumalar', 'url': 'http://twitter.com/search?q=%23Hay%C4%B1rl%C4%B1Cumalar', 'promoted_content': None, 'query': '%23Hay%C4%B1rl%C4%B1Cumalar', 'tweet_volume': 19848}, {'name': '#HayırlıKandiller', 'url': 'http://twitter.com/search?q=%23Hay%C4%B1rl%C4%B1Kandiller', 'promoted_content': None, 'query': '%23Hay%C4%B1rl%C4%B1Kandiller', 'tweet_volume': None}, {'name': '#HanumanJayanti', 'url': 'http://twitter.com/search?q=%23HanumanJayanti', 'promoted_content': None, 'query': '%23HanumanJayanti', 'tweet_volume': 83138}, {'name': '#IndonesianElectionHeroes', 'url': 'http://twitter.com/search?q=%23IndonesianElectionHeroes', 'promoted_content': None, 'query': '%23IndonesianElectionHeroes', 'tweet_volume': 19664}, {'name': '#يوم_الجمعه', 'url': 'http://twitter.com/search?q=%23%D9%8A%D9%88%D9%85_%D8%A7%D9%84%D8%AC%D9%85%D8%B9%D9%87', 'promoted_content': None, 'query': '%23%D9%8A%D9%88%D9%85_%D8%A7%D9%84%D8%AC%D9%85%D8%B9%D9%87', 'tweet_volume': 80799}, {'name': '#NRLBulldogsSouths', 'url': 'http://twitter.com/search?q=%23NRLBulldogsSouths', 'promoted_content': None, 'query': '%23NRLBulldogsSouths', 'tweet_volume': None}, {'name': '#NikahUmurBerapa', 'url': 'http://twitter.com/search?q=%23NikahUmurBerapa', 'promoted_content': None, 'query': '%23NikahUmurBerapa', 'tweet_volume': None}, {'name': '#DragRace', 'url': 'http://twitter.com/search?q=%23DragRace', 'promoted_content': None, 'query': '%23DragRace', 'tweet_volume': 37166}, {'name': '#ViernesSanto', 'url': 'http://twitter.com/search?q=%23ViernesSanto', 'promoted_content': None, 'query': '%23ViernesSanto', 'tweet_volume': None}, {'name': '#HardikPatel', 'url': 'http://twitter.com/search?q=%23HardikPatel', 'promoted_content': None, 'query': '%23HardikPatel', 'tweet_volume': None}, {'name': '#BLACKPINKxCorden', 'url': 'http://twitter.com/search?q=%23BLACKPINKxCorden', 'promoted_content': None, 'query': '%23BLACKPINKxCorden', 'tweet_volume': 253605}, {'name': '#Ontas', 'url': 'http://twitter.com/search?q=%23Ontas', 'promoted_content': None, 'query': '%23Ontas', 'tweet_volume': 27924}, {'name': '#ConCalmaRemix', 'url': 'http://twitter.com/search?q=%23ConCalmaRemix', 'promoted_content': None, 'query': '%23ConCalmaRemix', 'tweet_volume': 37846}, {'name': '#ProtestoEdiyorum', 'url': 'http://twitter.com/search?q=%23ProtestoEdiyorum', 'promoted_content': None, 'query': '%23ProtestoEdiyorum', 'tweet_volume': None}, {'name': '#DinahJane1', 'url': 'http://twitter.com/search?q=%23DinahJane1', 'promoted_content': None, 'query': '%23DinahJane1', 'tweet_volume': 23757}, {'name': '#ShivSena', 'url': 'http://twitter.com/search?q=%23ShivSena', 'promoted_content': None, 'query': '%23ShivSena', 'tweet_volume': None}, {'name': '#DuyguAsena', 'url': 'http://twitter.com/search?q=%23DuyguAsena', 'promoted_content': None, 'query': '%23DuyguAsena', 'tweet_volume': None}, {'name': '#TheJudasInMyLife', 'url': 'http://twitter.com/search?q=%23TheJudasInMyLife', 'promoted_content': None, 'query': '%23TheJudasInMyLife', 'tweet_volume': None}, {'name': '#Jersey', 'url': 'http://twitter.com/search?q=%23Jersey', 'promoted_content': None, 'query': '%23Jersey', 'tweet_volume': 20509}, {'name': '#اغلاق_BBM', 'url': 'http://twitter.com/search?q=%23%D8%A7%D8%BA%D9%84%D8%A7%D9%82_BBM', 'promoted_content': None, 'query': '%23%D8%A7%D8%BA%D9%84%D8%A7%D9%82_BBM', 'tweet_volume': 17055}, {'name': '#19aprile', 'url': 'http://twitter.com/search?q=%2319aprile', 'promoted_content': None, 'query': '%2319aprile', 'tweet_volume': None}, {'name': '#CHIvLIO', 'url': 'http://twitter.com/search?q=%23CHIvLIO', 'promoted_content': None, 'query': '%23CHIvLIO', 'tweet_volume': None}, {'name': '#Karfreitag', 'url': 'http://twitter.com/search?q=%23Karfreitag', 'promoted_content': None, 'query': '%23Karfreitag', 'tweet_volume': None}, {'name': '#JunquerasACN', 'url': 'http://twitter.com/search?q=%23JunquerasACN', 'promoted_content': None, 'query': '%23JunquerasACN', 'tweet_volume': None}], 'as_of': '2019-04-19T08:43:43Z', 'created_at': '2019-04-19T08:39:15Z', 'locations': [{'name': 'Worldwide', 'woeid': 1}]}]
    [{'trends': [{'name': '#WeLoveTheEarth', 'url': 'http://twitter.com/search?q=%23WeLoveTheEarth', 'promoted_content': None, 'query': '%23WeLoveTheEarth', 'tweet_volume': 159698}, {'name': '#DragRace', 'url': 'http://twitter.com/search?q=%23DragRace', 'promoted_content': None, 'query': '%23DragRace', 'tweet_volume': 37166}, {'name': 'Lil Dicky', 'url': 'http://twitter.com/search?q=%22Lil+Dicky%22', 'promoted_content': None, 'query': '%22Lil+Dicky%22', 'tweet_volume': 42461}, {'name': 'Derrick White', 'url': 'http://twitter.com/search?q=%22Derrick+White%22', 'promoted_content': None, 'query': '%22Derrick+White%22', 'tweet_volume': 27104}, {'name': '#CUZILOVEYOU', 'url': 'http://twitter.com/search?q=%23CUZILOVEYOU', 'promoted_content': None, 'query': '%23CUZILOVEYOU', 'tweet_volume': None}, {'name': 'Kevin Durant', 'url': 'http://twitter.com/search?q=%22Kevin+Durant%22', 'promoted_content': None, 'query': '%22Kevin+Durant%22', 'tweet_volume': 21870}, {'name': '#StarTrekDiscovery', 'url': 'http://twitter.com/search?q=%23StarTrekDiscovery', 'promoted_content': None, 'query': '%23StarTrekDiscovery', 'tweet_volume': None}, {'name': '#GSWvsLAC', 'url': 'http://twitter.com/search?q=%23GSWvsLAC', 'promoted_content': None, 'query': '%23GSWvsLAC', 'tweet_volume': None}, {'name': 'Oshie', 'url': 'http://twitter.com/search?q=Oshie', 'promoted_content': None, 'query': 'Oshie', 'tweet_volume': None}, {'name': 'Seth Abramson', 'url': 'http://twitter.com/search?q=%22Seth+Abramson%22', 'promoted_content': None, 'query': '%22Seth+Abramson%22', 'tweet_volume': None}, {'name': 'Lyra McKee', 'url': 'http://twitter.com/search?q=%22Lyra+McKee%22', 'promoted_content': None, 'query': '%22Lyra+McKee%22', 'tweet_volume': 17606}, {'name': 'Silky', 'url': 'http://twitter.com/search?q=Silky', 'promoted_content': None, 'query': 'Silky', 'tweet_volume': 12881}, {'name': 'Kazuo Koike', 'url': 'http://twitter.com/search?q=%22Kazuo+Koike%22', 'promoted_content': None, 'query': '%22Kazuo+Koike%22', 'tweet_volume': None}, {'name': 'Game 6', 'url': 'http://twitter.com/search?q=%22Game+6%22', 'promoted_content': None, 'query': '%22Game+6%22', 'tweet_volume': None}, {'name': 'Yvie', 'url': 'http://twitter.com/search?q=Yvie', 'promoted_content': None, 'query': 'Yvie', 'tweet_volume': 10680}, {'name': 'Gallant', 'url': 'http://twitter.com/search?q=Gallant', 'promoted_content': None, 'query': 'Gallant', 'tweet_volume': None}, {'name': 'Lone Wolf and Cub', 'url': 'http://twitter.com/search?q=%22Lone+Wolf+and+Cub%22', 'promoted_content': None, 'query': '%22Lone+Wolf+and+Cub%22', 'tweet_volume': None}, {'name': 'George Conway', 'url': 'http://twitter.com/search?q=%22George+Conway%22', 'promoted_content': None, 'query': '%22George+Conway%22', 'tweet_volume': 27458}, {'name': 'David Fletcher', 'url': 'http://twitter.com/search?q=%22David+Fletcher%22', 'promoted_content': None, 'query': '%22David+Fletcher%22', 'tweet_volume': None}, {'name': 'Derry', 'url': 'http://twitter.com/search?q=Derry', 'promoted_content': None, 'query': 'Derry', 'tweet_volume': 28234}, {'name': 'Mike Anderson', 'url': 'http://twitter.com/search?q=%22Mike+Anderson%22', 'promoted_content': None, 'query': '%22Mike+Anderson%22', 'tweet_volume': None}, {'name': 'Shy Glizzy', 'url': 'http://twitter.com/search?q=%22Shy+Glizzy%22', 'promoted_content': None, 'query': '%22Shy+Glizzy%22', 'tweet_volume': None}, {'name': 'Tomas Hertl', 'url': 'http://twitter.com/search?q=%22Tomas+Hertl%22', 'promoted_content': None, 'query': '%22Tomas+Hertl%22', 'tweet_volume': None}, {'name': 'Servais', 'url': 'http://twitter.com/search?q=Servais', 'promoted_content': None, 'query': 'Servais', 'tweet_volume': None}, {'name': 'WE LOVE THE EARTH', 'url': 'http://twitter.com/search?q=%22WE+LOVE+THE+EARTH%22', 'promoted_content': None, 'query': '%22WE+LOVE+THE+EARTH%22', 'tweet_volume': None}, {'name': '"Earth"', 'url': 'http://twitter.com/search?q=%22Earth%22', 'promoted_content': None, 'query': '%22Earth%22', 'tweet_volume': 338417}, {'name': '#DinahJane1', 'url': 'http://twitter.com/search?q=%23DinahJane1', 'promoted_content': None, 'query': '%23DinahJane1', 'tweet_volume': 23757}, {'name': '#WhatStopsYouFromGoingHome', 'url': 'http://twitter.com/search?q=%23WhatStopsYouFromGoingHome', 'promoted_content': None, 'query': '%23WhatStopsYouFromGoingHome', 'tweet_volume': None}, {'name': '#MakeAMovieSensual', 'url': 'http://twitter.com/search?q=%23MakeAMovieSensual', 'promoted_content': None, 'query': '%23MakeAMovieSensual', 'tweet_volume': None}, {'name': '#DontChangeOutNow', 'url': 'http://twitter.com/search?q=%23DontChangeOutNow', 'promoted_content': None, 'query': '%23DontChangeOutNow', 'tweet_volume': None}, {'name': '#BLACKPINKxCorden', 'url': 'http://twitter.com/search?q=%23BLACKPINKxCorden', 'promoted_content': None, 'query': '%23BLACKPINKxCorden', 'tweet_volume': 253605}, {'name': '#WorldofWarcraftMains', 'url': 'http://twitter.com/search?q=%23WorldofWarcraftMains', 'promoted_content': None, 'query': '%23WorldofWarcraftMains', 'tweet_volume': None}, {'name': '#MyDrunkUncleSays', 'url': 'http://twitter.com/search?q=%23MyDrunkUncleSays', 'promoted_content': None, 'query': '%23MyDrunkUncleSays', 'tweet_volume': None}, {'name': '#WGAMIX', 'url': 'http://twitter.com/search?q=%23WGAMIX', 'promoted_content': None, 'query': '%23WGAMIX', 'tweet_volume': None}, {'name': '#Earth', 'url': 'http://twitter.com/search?q=%23Earth', 'promoted_content': None, 'query': '%23Earth', 'tweet_volume': 13655}, {'name': '#TheLegendOfVoxMachina', 'url': 'http://twitter.com/search?q=%23TheLegendOfVoxMachina', 'promoted_content': None, 'query': '%23TheLegendOfVoxMachina', 'tweet_volume': None}, {'name': '#AFLNorthDons', 'url': 'http://twitter.com/search?q=%23AFLNorthDons', 'promoted_content': None, 'query': '%23AFLNorthDons', 'tweet_volume': None}, {'name': '#FridayFeeling', 'url': 'http://twitter.com/search?q=%23FridayFeeling', 'promoted_content': None, 'query': '%23FridayFeeling', 'tweet_volume': 19510}, {'name': '#MyInnerDemonSaid', 'url': 'http://twitter.com/search?q=%23MyInnerDemonSaid', 'promoted_content': None, 'query': '%23MyInnerDemonSaid', 'tweet_volume': None}, {'name': '#rupaulsdragrace', 'url': 'http://twitter.com/search?q=%23rupaulsdragrace', 'promoted_content': None, 'query': '%23rupaulsdragrace', 'tweet_volume': None}, {'name': '#ConCalmaRemix', 'url': 'http://twitter.com/search?q=%23ConCalmaRemix', 'promoted_content': None, 'query': '%23ConCalmaRemix', 'tweet_volume': 37846}, {'name': '#TimeToImpeach', 'url': 'http://twitter.com/search?q=%23TimeToImpeach', 'promoted_content': None, 'query': '%23TimeToImpeach', 'tweet_volume': 21732}, {'name': '#NRLBulldogsSouths', 'url': 'http://twitter.com/search?q=%23NRLBulldogsSouths', 'promoted_content': None, 'query': '%23NRLBulldogsSouths', 'tweet_volume': None}, {'name': '#CriticalRoleSpoilers', 'url': 'http://twitter.com/search?q=%23CriticalRoleSpoilers', 'promoted_content': None, 'query': '%23CriticalRoleSpoilers', 'tweet_volume': None}, {'name': '#GossipShouldBe', 'url': 'http://twitter.com/search?q=%23GossipShouldBe', 'promoted_content': None, 'query': '%23GossipShouldBe', 'tweet_volume': None}, {'name': '#LilDicky', 'url': 'http://twitter.com/search?q=%23LilDicky', 'promoted_content': None, 'query': '%23LilDicky', 'tweet_volume': None}, {'name': '#RPDR', 'url': 'http://twitter.com/search?q=%23RPDR', 'promoted_content': None, 'query': '%23RPDR', 'tweet_volume': None}, {'name': '#WeirdDateStories', 'url': 'http://twitter.com/search?q=%23WeirdDateStories', 'promoted_content': None, 'query': '%23WeirdDateStories', 'tweet_volume': None}, {'name': '#HustleAndSoul', 'url': 'http://twitter.com/search?q=%23HustleAndSoul', 'promoted_content': None, 'query': '%23HustleAndSoul', 'tweet_volume': None}, {'name': '#fridaymotivation', 'url': 'http://twitter.com/search?q=%23fridaymotivation', 'promoted_content': None, 'query': '%23fridaymotivation', 'tweet_volume': None}], 'as_of': '2019-04-19T08:43:43Z', 'created_at': '2019-04-19T08:39:15Z', 'locations': [{'name': 'United States', 'woeid': 23424977}]}]

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_pandas_loaded():
    assert 'json' in globals(), \
    'Did you import the json module?'
    
def test_WW_trends_correctly_loaded():
    correct_ww_trends = json.loads(open('datasets/WWTrends.json').read())
    assert correct_ww_trends == WW_trends, "The variable WW_trends should contain the data in WWTrends.json."

def test_US_trends_correctly_loaded():
    correct_us_trends = json.loads(open('datasets/USTrends.json').read())
    assert correct_us_trends == US_trends, "The variable WW_trends should contain the data in USTrends.json."
```

    3/3 tests passed

## 2. Prettifying the output
<p>Our data was hard to read! Luckily, we can resort to the <i>json.dumps()</i> method to have it formatted as a pretty JSON string.</p>

```python
# Pretty-printing the results. First WW and then US trends.

print("WW trends:")
json.dumps(WW_trends, indent=1)

print("\n", "US trends:")
json.dumps(US_trends, indent=1)
```

    WW trends:
    
     US trends:

    '[\n {\n  "trends": [\n   {\n    "name": "#WeLoveTheEarth",\n    "url": "http://twitter.com/search?q=%23WeLoveTheEarth",\n    "promoted_content": null,\n    "query": "%23WeLoveTheEarth",\n    "tweet_volume": 159698\n   },\n   {\n    "name": "#DragRace",\n    "url": "http://twitter.com/search?q=%23DragRace",\n    "promoted_content": null,\n    "query": "%23DragRace",\n    "tweet_volume": 37166\n   },\n   {\n    "name": "Lil Dicky",\n    "url": "http://twitter.com/search?q=%22Lil+Dicky%22",\n    "promoted_content": null,\n    "query": "%22Lil+Dicky%22",\n    "tweet_volume": 42461\n   },\n   {\n    "name": "Derrick White",\n    "url": "http://twitter.com/search?q=%22Derrick+White%22",\n    "promoted_content": null,\n    "query": "%22Derrick+White%22",\n    "tweet_volume": 27104\n   },\n   {\n    "name": "#CUZILOVEYOU",\n    "url": "http://twitter.com/search?q=%23CUZILOVEYOU",\n    "promoted_content": null,\n    "query": "%23CUZILOVEYOU",\n    "tweet_volume": null\n   },\n   {\n    "name": "Kevin Durant",\n    "url": "http://twitter.com/search?q=%22Kevin+Durant%22",\n    "promoted_content": null,\n    "query": "%22Kevin+Durant%22",\n    "tweet_volume": 21870\n   },\n   {\n    "name": "#StarTrekDiscovery",\n    "url": "http://twitter.com/search?q=%23StarTrekDiscovery",\n    "promoted_content": null,\n    "query": "%23StarTrekDiscovery",\n    "tweet_volume": null\n   },\n   {\n    "name": "#GSWvsLAC",\n    "url": "http://twitter.com/search?q=%23GSWvsLAC",\n    "promoted_content": null,\n    "query": "%23GSWvsLAC",\n    "tweet_volume": null\n   },\n   {\n    "name": "Oshie",\n    "url": "http://twitter.com/search?q=Oshie",\n    "promoted_content": null,\n    "query": "Oshie",\n    "tweet_volume": null\n   },\n   {\n    "name": "Seth Abramson",\n    "url": "http://twitter.com/search?q=%22Seth+Abramson%22",\n    "promoted_content": null,\n    "query": "%22Seth+Abramson%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Lyra McKee",\n    "url": "http://twitter.com/search?q=%22Lyra+McKee%22",\n    "promoted_content": null,\n    "query": "%22Lyra+McKee%22",\n    "tweet_volume": 17606\n   },\n   {\n    "name": "Silky",\n    "url": "http://twitter.com/search?q=Silky",\n    "promoted_content": null,\n    "query": "Silky",\n    "tweet_volume": 12881\n   },\n   {\n    "name": "Kazuo Koike",\n    "url": "http://twitter.com/search?q=%22Kazuo+Koike%22",\n    "promoted_content": null,\n    "query": "%22Kazuo+Koike%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Game 6",\n    "url": "http://twitter.com/search?q=%22Game+6%22",\n    "promoted_content": null,\n    "query": "%22Game+6%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Yvie",\n    "url": "http://twitter.com/search?q=Yvie",\n    "promoted_content": null,\n    "query": "Yvie",\n    "tweet_volume": 10680\n   },\n   {\n    "name": "Gallant",\n    "url": "http://twitter.com/search?q=Gallant",\n    "promoted_content": null,\n    "query": "Gallant",\n    "tweet_volume": null\n   },\n   {\n    "name": "Lone Wolf and Cub",\n    "url": "http://twitter.com/search?q=%22Lone+Wolf+and+Cub%22",\n    "promoted_content": null,\n    "query": "%22Lone+Wolf+and+Cub%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "George Conway",\n    "url": "http://twitter.com/search?q=%22George+Conway%22",\n    "promoted_content": null,\n    "query": "%22George+Conway%22",\n    "tweet_volume": 27458\n   },\n   {\n    "name": "David Fletcher",\n    "url": "http://twitter.com/search?q=%22David+Fletcher%22",\n    "promoted_content": null,\n    "query": "%22David+Fletcher%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Derry",\n    "url": "http://twitter.com/search?q=Derry",\n    "promoted_content": null,\n    "query": "Derry",\n    "tweet_volume": 28234\n   },\n   {\n    "name": "Mike Anderson",\n    "url": "http://twitter.com/search?q=%22Mike+Anderson%22",\n    "promoted_content": null,\n    "query": "%22Mike+Anderson%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Shy Glizzy",\n    "url": "http://twitter.com/search?q=%22Shy+Glizzy%22",\n    "promoted_content": null,\n    "query": "%22Shy+Glizzy%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Tomas Hertl",\n    "url": "http://twitter.com/search?q=%22Tomas+Hertl%22",\n    "promoted_content": null,\n    "query": "%22Tomas+Hertl%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "Servais",\n    "url": "http://twitter.com/search?q=Servais",\n    "promoted_content": null,\n    "query": "Servais",\n    "tweet_volume": null\n   },\n   {\n    "name": "WE LOVE THE EARTH",\n    "url": "http://twitter.com/search?q=%22WE+LOVE+THE+EARTH%22",\n    "promoted_content": null,\n    "query": "%22WE+LOVE+THE+EARTH%22",\n    "tweet_volume": null\n   },\n   {\n    "name": "\\"Earth\\"",\n    "url": "http://twitter.com/search?q=%22Earth%22",\n    "promoted_content": null,\n    "query": "%22Earth%22",\n    "tweet_volume": 338417\n   },\n   {\n    "name": "#DinahJane1",\n    "url": "http://twitter.com/search?q=%23DinahJane1",\n    "promoted_content": null,\n    "query": "%23DinahJane1",\n    "tweet_volume": 23757\n   },\n   {\n    "name": "#WhatStopsYouFromGoingHome",\n    "url": "http://twitter.com/search?q=%23WhatStopsYouFromGoingHome",\n    "promoted_content": null,\n    "query": "%23WhatStopsYouFromGoingHome",\n    "tweet_volume": null\n   },\n   {\n    "name": "#MakeAMovieSensual",\n    "url": "http://twitter.com/search?q=%23MakeAMovieSensual",\n    "promoted_content": null,\n    "query": "%23MakeAMovieSensual",\n    "tweet_volume": null\n   },\n   {\n    "name": "#DontChangeOutNow",\n    "url": "http://twitter.com/search?q=%23DontChangeOutNow",\n    "promoted_content": null,\n    "query": "%23DontChangeOutNow",\n    "tweet_volume": null\n   },\n   {\n    "name": "#BLACKPINKxCorden",\n    "url": "http://twitter.com/search?q=%23BLACKPINKxCorden",\n    "promoted_content": null,\n    "query": "%23BLACKPINKxCorden",\n    "tweet_volume": 253605\n   },\n   {\n    "name": "#WorldofWarcraftMains",\n    "url": "http://twitter.com/search?q=%23WorldofWarcraftMains",\n    "promoted_content": null,\n    "query": "%23WorldofWarcraftMains",\n    "tweet_volume": null\n   },\n   {\n    "name": "#MyDrunkUncleSays",\n    "url": "http://twitter.com/search?q=%23MyDrunkUncleSays",\n    "promoted_content": null,\n    "query": "%23MyDrunkUncleSays",\n    "tweet_volume": null\n   },\n   {\n    "name": "#WGAMIX",\n    "url": "http://twitter.com/search?q=%23WGAMIX",\n    "promoted_content": null,\n    "query": "%23WGAMIX",\n    "tweet_volume": null\n   },\n   {\n    "name": "#Earth",\n    "url": "http://twitter.com/search?q=%23Earth",\n    "promoted_content": null,\n    "query": "%23Earth",\n    "tweet_volume": 13655\n   },\n   {\n    "name": "#TheLegendOfVoxMachina",\n    "url": "http://twitter.com/search?q=%23TheLegendOfVoxMachina",\n    "promoted_content": null,\n    "query": "%23TheLegendOfVoxMachina",\n    "tweet_volume": null\n   },\n   {\n    "name": "#AFLNorthDons",\n    "url": "http://twitter.com/search?q=%23AFLNorthDons",\n    "promoted_content": null,\n    "query": "%23AFLNorthDons",\n    "tweet_volume": null\n   },\n   {\n    "name": "#FridayFeeling",\n    "url": "http://twitter.com/search?q=%23FridayFeeling",\n    "promoted_content": null,\n    "query": "%23FridayFeeling",\n    "tweet_volume": 19510\n   },\n   {\n    "name": "#MyInnerDemonSaid",\n    "url": "http://twitter.com/search?q=%23MyInnerDemonSaid",\n    "promoted_content": null,\n    "query": "%23MyInnerDemonSaid",\n    "tweet_volume": null\n   },\n   {\n    "name": "#rupaulsdragrace",\n    "url": "http://twitter.com/search?q=%23rupaulsdragrace",\n    "promoted_content": null,\n    "query": "%23rupaulsdragrace",\n    "tweet_volume": null\n   },\n   {\n    "name": "#ConCalmaRemix",\n    "url": "http://twitter.com/search?q=%23ConCalmaRemix",\n    "promoted_content": null,\n    "query": "%23ConCalmaRemix",\n    "tweet_volume": 37846\n   },\n   {\n    "name": "#TimeToImpeach",\n    "url": "http://twitter.com/search?q=%23TimeToImpeach",\n    "promoted_content": null,\n    "query": "%23TimeToImpeach",\n    "tweet_volume": 21732\n   },\n   {\n    "name": "#NRLBulldogsSouths",\n    "url": "http://twitter.com/search?q=%23NRLBulldogsSouths",\n    "promoted_content": null,\n    "query": "%23NRLBulldogsSouths",\n    "tweet_volume": null\n   },\n   {\n    "name": "#CriticalRoleSpoilers",\n    "url": "http://twitter.com/search?q=%23CriticalRoleSpoilers",\n    "promoted_content": null,\n    "query": "%23CriticalRoleSpoilers",\n    "tweet_volume": null\n   },\n   {\n    "name": "#GossipShouldBe",\n    "url": "http://twitter.com/search?q=%23GossipShouldBe",\n    "promoted_content": null,\n    "query": "%23GossipShouldBe",\n    "tweet_volume": null\n   },\n   {\n    "name": "#LilDicky",\n    "url": "http://twitter.com/search?q=%23LilDicky",\n    "promoted_content": null,\n    "query": "%23LilDicky",\n    "tweet_volume": null\n   },\n   {\n    "name": "#RPDR",\n    "url": "http://twitter.com/search?q=%23RPDR",\n    "promoted_content": null,\n    "query": "%23RPDR",\n    "tweet_volume": null\n   },\n   {\n    "name": "#WeirdDateStories",\n    "url": "http://twitter.com/search?q=%23WeirdDateStories",\n    "promoted_content": null,\n    "query": "%23WeirdDateStories",\n    "tweet_volume": null\n   },\n   {\n    "name": "#HustleAndSoul",\n    "url": "http://twitter.com/search?q=%23HustleAndSoul",\n    "promoted_content": null,\n    "query": "%23HustleAndSoul",\n    "tweet_volume": null\n   },\n   {\n    "name": "#fridaymotivation",\n    "url": "http://twitter.com/search?q=%23fridaymotivation",\n    "promoted_content": null,\n    "query": "%23fridaymotivation",\n    "tweet_volume": null\n   }\n  ],\n  "as_of": "2019-04-19T08:43:43Z",\n  "created_at": "2019-04-19T08:39:15Z",\n  "locations": [\n   {\n    "name": "United States",\n    "woeid": 23424977\n   }\n  ]\n }\n]'


```python
# Not sure what to check here

# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_info_command():
    assert 'json.dumps(WW_trends' in last_input, \
        "We expected the json.dumps method with the correct input object."
    assert 'json.dumps(US_trends' in last_input, \
         "We expected the json.dumps method with the correct input object."
```

    1/1 tests passed

## 3.  Finding common trends
<p>🕵️‍♀️ From the pretty-printed results (output of the previous task), we can observe that:</p>
<ul>
<li><p>We have an array of trend objects having: the name of the trending topic, the query parameter that can be used to search for the topic on Twitter-Search, the search URL and the volume of tweets for the last 24 hours, if available. (The trends get updated every 5 mins.)</p></li>
<li><p>At query time <b><i>#BeratKandili, #GoodFriday</i></b> and <b><i>#WeLoveTheEarth</i></b> were trending WW.</p></li>
<li><p><i>"tweet_volume"</i> tell us that <i>#WeLoveTheEarth</i> was the most popular among the three.</p></li>
<li><p>Results are not sorted by <i>"tweet_volume"</i>. </p></li>
<li><p>There are some trends which are unique to the US.</p></li>
</ul>
<hr>
<p>It’s easy to skim through the two sets of trends and spot common trends, but let's not do "manual" work. We can use Python’s <strong>set</strong> data structure to find common trends — we can iterate through the two trends objects, cast the lists of names to sets, and call the intersection method to get the common names between the two sets.</p>

```python
# Extracting all the WW trend names from WW_trends
world_trends = set([trend['name'] for trend in WW_trends[0]['trends']])

# Extracting all the US trend names from US_trends
us_trends = set([trend['name'] for trend in US_trends[0]['trends']]) 

# Getting the intersection of the two sets of trends
common_trends = world_trends.intersection(us_trends)

# Inspecting the data
print(world_trends, "\n")
print(us_trends, "\n")
print (len(common_trends), "common trends:", common_trends)
```

    {'刀ステ', '池袋の事故', '高齢者', '#TheJudasInMyLife', '十二国記', 'Hemant Karkare', '#19aprile', '重体の女性と女児', '브이알', '#HanumanJayanti', 'Derrick White', '#BeratKandili', '#ShivSena', 'Priyanka Chaturvedi', '#HayırlıKandiller', '歩行者', '#AFLNorthDons', '#NRLBulldogsSouths', '#Ontas', 'Lyra McKee', '#DinahJane1', '#JunquerasACN', 'Shiv Sena', 'プリウス', '免許返納', 'グレア', '#GoodFriday', '#HardikPatel', '#ConCalmaRemix', '#DragRace', '#يوم_الجمعه', '#ViernesSanto', '#WeLoveTheEarth', '#KpuJanganCurang', 'örgütdeğil arkadaşgrubu', 'Derry', 'Lil Dicky', '#ProtestoEdiyorum', '#DuyguAsena', '#Karfreitag', '#NikahUmurBerapa', '#اغلاق_BBM', '#BLACKPINKxCorden', '東京・池袋衝突事故', '#195TLdenTTVerilir', '#HayırlıCumalar', '#Jersey', 'Berat Kandilimiz', '#CHIvLIO', '#IndonesianElectionHeroes'} 
    
    {'Game 6', '#WhatStopsYouFromGoingHome', '#WorldofWarcraftMains', '#WeirdDateStories', 'Lone Wolf and Cub', '#TimeToImpeach', '#TheLegendOfVoxMachina', '"Earth"', '#CriticalRoleSpoilers', 'George Conway', 'Derrick White', '#MyDrunkUncleSays', '#NRLBulldogsSouths', '#AFLNorthDons', '#StarTrekDiscovery', 'Lyra McKee', '#DinahJane1', '#LilDicky', 'Seth Abramson', '#fridaymotivation', '#GSWvsLAC', '#WGAMIX', '#DontChangeOutNow', 'David Fletcher', '#FridayFeeling', '#ConCalmaRemix', '#RPDR', '#DragRace', '#CUZILOVEYOU', 'Servais', '#WeLoveTheEarth', 'Derry', 'WE LOVE THE EARTH', '#GossipShouldBe', '#rupaulsdragrace', 'Lil Dicky', 'Silky', '#HustleAndSoul', 'Gallant', 'Mike Anderson', 'Tomas Hertl', 'Oshie', '#BLACKPINKxCorden', 'Kazuo Koike', 'Shy Glizzy', 'Kevin Durant', '#MakeAMovieSensual', '#Earth', '#MyInnerDemonSaid', 'Yvie'} 
    
    11 common trends: {'Lil Dicky', '#NRLBulldogsSouths', '#AFLNorthDons', '#ConCalmaRemix', '#DragRace', 'Lyra McKee', '#DinahJane1', '#BLACKPINKxCorden', '#WeLoveTheEarth', 'Derry', 'Derrick White'}

```python
# One or more tests of the students code. 
# The @solution should pass the tests.
# The purpose of the tests is to try to catch common errors and to 
# give the student a hint on how to resolve these errors.

def test_ww_trends():
    correct_world_trends = set([trend['name'] for trend in WW_trends[0]['trends']])
    assert world_trends == correct_world_trends, \
    'The variable world_trends does not have the expected trend names.'
   
def test_us_trends():
    correct_us_trends = set([trend['name'] for trend in US_trends[0]['trends']])
    assert us_trends == correct_us_trends, \
    'The variable us_trends does not have the expected trend names.'

def test_common_trends():
    correct_common_trends = world_trends.intersection(us_trends)
    assert common_trends == correct_common_trends, \
    'The variable common_trends does not have the expected common trend names.'
```

    3/3 tests passed

## 4. Exploring the hot trend
<p>🕵️‍♀️ From the intersection (last output) we can see that, out of the two sets of trends (each of size 50), we have 11 overlapping topics. In particular, there is one common trend that sounds very interesting: <i><b>#WeLoveTheEarth</b></i> — so good to see that <em>Twitteratis</em> are unanimously talking about loving Mother Earth! 💚 </p>
<p><i><b>Note</b>: We could have had no overlap or a much higher overlap; when we did the query for getting the trends, people in the US could have been on fire obout topics only relevant to them.</i>
<br>
<img src="https://assets.datacamp.com/production/project_760/img/earth.jpg" style="width: 500px"></p>
<div style="text-align: center;"><i>Image Source:Official Music Video Cover: https://welovetheearth.org/video/</i></div>
<hr>
<p>We have found a hot-trend, #WeLoveTheEarth. Now let's see what story it is screaming to tell us! <br>
If we query Twitter's search API with this hashtag as query parameter, we get back actual tweets related to it. We have the response from the search API stored in the datasets folder as <i>'WeLoveTheEarth.json'</i>. So let's load this dataset and do a deep dive in this trend.</p>

```python
# Loading the data
tweets = json.loads(open('datasets/WeLoveTheEarth.json').read())

# Inspecting some tweets
tweets[0:2]
```

    [{'created_at': 'Fri Apr 19 08:46:48 +0000 2019',
      'id': 1119160405270523904,
      'id_str': '1119160405270523904',
      'text': 'RT @lildickytweets: 🌎 out now #WeLoveTheEarth https://t.co/L22XsoT5P1',
      'truncated': False,
      'entities': {'hashtags': [{'text': 'WeLoveTheEarth', 'indices': [30, 45]}],
       'symbols': [],
       'user_mentions': [{'screen_name': 'lildickytweets',
         'name': 'LD',
         'id': 1209516660,
         'id_str': '1209516660',
         'indices': [3, 18]}],
       'urls': [{'url': 'https://t.co/L22XsoT5P1',
         'expanded_url': 'https://youtu.be/pvuN_WvF1to',
         'display_url': 'youtu.be/pvuN_WvF1to',
         'indices': [46, 69]}]},
      'metadata': {'iso_language_code': 'en', 'result_type': 'recent'},
      'source': '<a href="http://twitter.com/download/android" rel="nofollow">Twitter for Android</a>',
      'in_reply_to_status_id': None,
      'in_reply_to_status_id_str': None,
      'in_reply_to_user_id': None,
      'in_reply_to_user_id_str': None,
      'in_reply_to_screen_name': None,
      'user': {'id': 212375312,
       'id_str': '212375312',
       'name': 'fake smile',
       'screen_name': 'Pati95Poland',
       'location': 'SWAGLAND   ',
       'description': "''you just got knocked the fuck out''",
       'url': 'https://t.co/nxzlSyYZSK',
       'entities': {'url': {'urls': [{'url': 'https://t.co/nxzlSyYZSK',
           'expanded_url': 'http://loveeeujdb.tumblr.com/',
           'display_url': 'loveeeujdb.tumblr.com',
           'indices': [0, 23]}]},
        'description': {'urls': []}},
       'protected': False,
       'followers_count': 2306,
       'friends_count': 697,
       'listed_count': 28,
       'created_at': 'Fri Nov 05 22:25:29 +0000 2010',
       'favourites_count': 5552,
       'utc_offset': None,
       'time_zone': None,
       'geo_enabled': True,
       'verified': False,
       'statuses_count': 185750,
       'lang': 'pl',
       'contributors_enabled': False,
       'is_translator': False,
       'is_translation_enabled': False,
       'profile_background_color': 'FFFFFF',
       'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme18/bg.gif',
       'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme18/bg.gif',
       'profile_background_tile': False,
       'profile_image_url': 'http://pbs.twimg.com/profile_images/1093929135183937537/hQuxtwKq_normal.jpg',
       'profile_image_url_https': 'https://pbs.twimg.com/profile_images/1093929135183937537/hQuxtwKq_normal.jpg',
       'profile_banner_url': 'https://pbs.twimg.com/profile_banners/212375312/1522705183',
       'profile_link_color': 'ABB8C2',
       'profile_sidebar_border_color': 'FFFFFF',
       'profile_sidebar_fill_color': 'F6F6F6',
       'profile_text_color': '333333',
       'profile_use_background_image': True,
       'has_extended_profile': True,
       'default_profile': False,
       'default_profile_image': False,
       'following': False,
       'follow_request_sent': False,
       'notifications': False,
       'translator_type': 'regular'},
      'geo': None,
      'coordinates': None,
      'place': None,
      'contributors': None,
      'retweeted_status': {'created_at': 'Fri Apr 19 04:22:29 +0000 2019',
       'id': 1119093888524754946,
       'id_str': '1119093888524754946',
       'text': '🌎 out now #WeLoveTheEarth https://t.co/L22XsoT5P1',
       'truncated': False,
       'entities': {'hashtags': [{'text': 'WeLoveTheEarth', 'indices': [10, 25]}],
        'symbols': [],
        'user_mentions': [],
        'urls': [{'url': 'https://t.co/L22XsoT5P1',
          'expanded_url': 'https://youtu.be/pvuN_WvF1to',
          'display_url': 'youtu.be/pvuN_WvF1to',
          'indices': [26, 49]}]},
       'metadata': {'iso_language_code': 'en', 'result_type': 'recent'},
       'source': '<a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>',
       'in_reply_to_status_id': None,
       'in_reply_to_status_id_str': None,
       'in_reply_to_user_id': None,
       'in_reply_to_user_id_str': None,
       'in_reply_to_screen_name': None,
       'user': {'id': 1209516660,
        'id_str': '1209516660',
        'name': 'LD',
        'screen_name': 'lildickytweets',
        'location': 'Earth',
        'description': 'Rapper/Actor/Comedian/Model #WeLoveTheEarth',
        'url': 'https://t.co/aFrPkkJKqs',
        'entities': {'url': {'urls': [{'url': 'https://t.co/aFrPkkJKqs',
            'expanded_url': 'https://LilDicky.lnk.to/Earth',
            'display_url': 'LilDicky.lnk.to/Earth',
            'indices': [0, 23]}]},
         'description': {'urls': []}},
        'protected': False,
        'followers_count': 503111,
        'friends_count': 945,
        'listed_count': 657,
        'created_at': 'Fri Feb 22 19:06:15 +0000 2013',
        'favourites_count': 7696,
        'utc_offset': None,
        'time_zone': None,
        'geo_enabled': False,
        'verified': True,
        'statuses_count': 14430,
        'lang': 'en',
        'contributors_enabled': False,
        'is_translator': False,
        'is_translation_enabled': False,
        'profile_background_color': '000000',
        'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme14/bg.gif',
        'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme14/bg.gif',
        'profile_background_tile': False,
        'profile_image_url': 'http://pbs.twimg.com/profile_images/1119087366679846912/XSa4fpQA_normal.png',
        'profile_image_url_https': 'https://pbs.twimg.com/profile_images/1119087366679846912/XSa4fpQA_normal.png',
        'profile_banner_url': 'https://pbs.twimg.com/profile_banners/1209516660/1555646206',
        'profile_link_color': '858585',
        'profile_sidebar_border_color': 'FFFFFF',
        'profile_sidebar_fill_color': 'DDEEF6',
        'profile_text_color': '333333',
        'profile_use_background_image': True,
        'has_extended_profile': False,
        'default_profile': False,
        'default_profile_image': False,
        'following': False,
        'follow_request_sent': False,
        'notifications': False,
        'translator_type': 'none'},
       'geo': None,
       'coordinates': None,
       'place': None,
       'contributors': None,
       'is_quote_status': False,
       'retweet_count': 7482,
       'favorite_count': 13317,
       'favorited': False,
       'retweeted': False,
       'possibly_sensitive': False,
       'lang': 'en'},
      'is_quote_status': False,
      'retweet_count': 7482,
      'favorite_count': 0,
      'favorited': False,
      'retweeted': False,
      'possibly_sensitive': False,
      'lang': 'en'},
     {'created_at': 'Fri Apr 19 08:46:48 +0000 2019',
      'id': 1119160404876206080,
      'id_str': '1119160404876206080',
      'text': '💚🌎💚  #WeLoveTheEarth 👇🏼',
      'truncated': False,
      'entities': {'hashtags': [{'text': 'WeLoveTheEarth', 'indices': [5, 20]}],
       'symbols': [],
       'user_mentions': [],
       'urls': []},
      'metadata': {'iso_language_code': 'und', 'result_type': 'recent'},
      'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>',
      'in_reply_to_status_id': None,
      'in_reply_to_status_id_str': None,
      'in_reply_to_user_id': None,
      'in_reply_to_user_id_str': None,
      'in_reply_to_screen_name': None,
      'user': {'id': 72150460,
       'id_str': '72150460',
       'name': 'Alfonsina del Mar (Dianishka Prietishka)',
       'screen_name': 'Diana____X',
       'location': 'México',
       'description': '☸︎ ⚓︎ 👩🏻\u200d✈️ ★★★★ ♒︎',
       'url': None,
       'entities': {'description': {'urls': []}},
       'protected': False,
       'followers_count': 223,
       'friends_count': 513,
       'listed_count': 0,
       'created_at': 'Sun Sep 06 23:26:24 +0000 2009',
       'favourites_count': 750,
       'utc_offset': None,
       'time_zone': None,
       'geo_enabled': True,
       'verified': False,
       'statuses_count': 1668,
       'lang': 'es',
       'contributors_enabled': False,
       'is_translator': False,
       'is_translation_enabled': False,
       'profile_background_color': '642D8B',
       'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme10/bg.gif',
       'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme10/bg.gif',
       'profile_background_tile': True,
       'profile_image_url': 'http://pbs.twimg.com/profile_images/1072296818531278848/tgn0e2h4_normal.jpg',
       'profile_image_url_https': 'https://pbs.twimg.com/profile_images/1072296818531278848/tgn0e2h4_normal.jpg',
       'profile_banner_url': 'https://pbs.twimg.com/profile_banners/72150460/1545198367',
       'profile_link_color': '8400FF',
       'profile_sidebar_border_color': '65B0DA',
       'profile_sidebar_fill_color': '7AC3EE',
       'profile_text_color': '3D1957',
       'profile_use_background_image': True,
       'has_extended_profile': True,
       'default_profile': False,
       'default_profile_image': False,
       'following': False,
       'follow_request_sent': False,
       'notifications': False,
       'translator_type': 'none'},
      'geo': None,
      'coordinates': None,
      'place': None,
      'contributors': None,
      'is_quote_status': False,
      'retweet_count': 0,
      'favorite_count': 0,
      'favorited': False,
      'retweeted': False,
      'lang': 'und'}]

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_tweets_loaded_correctly():
    correct_tweets_data = json.loads(open('datasets/WeLoveTheEarth.json').read())
    assert correct_tweets_data == tweets, "The variable tweets should contain the data in WeLoveTheEarth.json."
    
```

    1/1 tests passed

## 5. Digging deeper
<p>🕵️‍♀️ Printing the first two tweet items makes us realize that there’s a lot more to a tweet than what we normally think of as a tweet — there is a lot more than just a short text!</p>
<hr>
<p>But hey, let's not get overwhemled by all the information in a tweet object! Let's focus on a few interesting fields and see if we can find any hidden insights there. </p>

```python
# Extracting the text of all the tweets from the tweet object
texts = [tweet['text'] for tweet in tweets]

# Extracting screen names of users tweeting about #WeLoveTheEarth
names = [hashtag['screen_name'] 
             for tweet in tweets
                 for hashtag in tweet['entities']['user_mentions']]

# Extracting all the hashtags being used when talking about this topic
hashtags = [hashtag['text'] 
             for tweet in tweets
                 for hashtag in tweet['entities']['hashtags']]

# Inspecting the first 10 results
print (json.dumps(texts[0:10], indent=1),"\n")
print (json.dumps(names[0:10], indent=1),"\n")
print (json.dumps(hashtags[0:10], indent=1),"\n")
```

    [
     "RT @lildickytweets: \ud83c\udf0e out now #WeLoveTheEarth https://t.co/L22XsoT5P1",
     "\ud83d\udc9a\ud83c\udf0e\ud83d\udc9a  #WeLoveTheEarth \ud83d\udc47\ud83c\udffc",
     "RT @cabeyoomoon: Ta piosenka to bop,  wpada w ucho  i dochody z niej id\u0105 na dobry cel,  warto s\u0142ucha\u0107 w k\u00f3\u0142ko i w k\u00f3\u0142ko gdziekolwiek si\u0119 ty\u2026",
     "#WeLoveTheEarth \nCzemu ja si\u0119 pop\u0142aka\u0142am",
     "RT @Spotify: This is epic. @lildickytweets got @justinbieber, @arianagrande, @halsey, @sanbenito, @edsheeran, @SnoopDogg, @ShawnMendes, @Kr\u2026",
     "RT @biebercentineo: Justin : are we gonna die? \nLil dicky: you know bieber we might die \n\nBTCH IM CRYING #EARTH #WeLoveTheEarth #WELOVEEART\u2026",
     "RT @dreamsiinflate: #WeLoveTheEarth \u201ci am a fat fucking pig\u201d okay brendon urie https://t.co/FdJmq31xZc",
     "Literally no one:\n\nMe in the past 4 hours:\n\nI'm a koala and I sleep all the time, so what, it's cute \ud83c\udfb6\n\n#WeLoveTheEarth #EdSheeranTheKoala",
     "RT @Yuuupthatsme: Mia\u0142e\u015b by\u0107 \u017cyraf\u0105 #WeLoveTheEarth https://t.co/0kNCpU8o6q",
     "RT @jaguareffects: eu prestando aten\u00e7\u00e3o no \u00e1udio pra identificar cada artista\n\n#WeLoveTheEarth https://t.co/0cDtiV2t1E"
    ] 
    
    [
     "lildickytweets",
     "cabeyoomoon",
     "Spotify",
     "lildickytweets",
     "justinbieber",
     "ArianaGrande",
     "halsey",
     "sanbenito",
     "edsheeran",
     "SnoopDogg"
    ] 
    
    [
     "WeLoveTheEarth",
     "WeLoveTheEarth",
     "WeLoveTheEarth",
     "EARTH",
     "WeLoveTheEarth",
     "WeLoveTheEarth",
     "WeLoveTheEarth",
     "EdSheeranTheKoala",
     "WeLoveTheEarth",
     "WeLoveTheEarth"
    ] 

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_extracted_texts():
    correct_text = [tweet['text'] for tweet in tweets ]
    assert texts == correct_text, \
    'The variable texts does not have the expected text data.'
   
def test_extracted_names():
    correct_names = [user_mention['screen_name'] 
                         for tweet in tweets 
                             for user_mention in tweet['entities']['user_mentions']]
    assert correct_names == names, \
    'The variable names does not have the expected user names.'
    
def test_extracted_hashtags():
    correct_hashtags = [hashtag['text'] 
                            for tweet in tweets
                                 for hashtag in tweet['entities']['hashtags']]
    assert correct_hashtags == hashtags, \
    'The variable hashtags does not have the expected hashtag data.'
```

    3/3 tests passed

## 6. Frequency analysis
<p>🕵️‍♀️ Just from the first few results of the last extraction, we can deduce that:</p>
<ul>
<li>We are talking about a song about loving the Earth.</li>
<li>A lot of big artists are the forces behind this Twitter wave, especially Lil Dicky.</li>
<li>Ed Sheeran was some cute koala in the song — "EdSheeranTheKoala" hashtag! 🐨</li>
</ul>
<hr>
<p>Observing the first 10 items of the interesting fields gave us a sense of the data. We can now take a closer look by doing a simple, but very useful, exercise — computing frequency distributions. Starting simple with frequencies is generally a good approach; it helps in getting ideas about how to proceed further.</p>

```python
# Importing modules
from collections import Counter

# Counting occcurrences/ getting frequency dist of all names and hashtags
for item in [names, hashtags]:
    c = Counter(item) 
    # Inspecting the 10 most common items in c
    print (c.most_common(10), "\n")
```

    [('lildickytweets', 102), ('LeoDiCaprio', 44), ('ShawnMendes', 33), ('halsey', 31), ('ArianaGrande', 30), ('justinbieber', 29), ('Spotify', 26), ('edsheeran', 26), ('sanbenito', 25), ('SnoopDogg', 25)] 
    
    [('WeLoveTheEarth', 313), ('4future', 12), ('19aprile', 12), ('EARTH', 11), ('fridaysforfuture', 10), ('EarthMusicVideo', 3), ('ConCalmaRemix', 3), ('Earth', 3), ('aliens', 2), ('AvengersEndgame', 2)] 

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_counter():
    for item in [names, hashtags]: correct_counter = Counter(item)  
    assert c == correct_counter, \
    "The variable c does not have the expected values."
```

    1/1 tests passed

## 7. Activity around the trend
<p>🕵️‍♀️ Based on the last frequency distributions we can further build-up on our deductions:</p>
<ul>
<li>We can more safely say that this was a music video about Earth (hashtag 'EarthMusicVideo') by Lil Dicky. </li>
<li>DiCaprio is not a music artist, but he was involved as well <em>(Leo is an environmentalist so not a surprise to see his name pop up here)</em>. </li>
<li>We can also say that the video was released on a Friday; very likely on April 19th. </li>
</ul>
<p><em>We have been able to extract so many insights. Quite powerful, isn't it?!</em></p>
<hr>
<p>Let's further analyze the data to find patterns in the activity around the tweets — <b>did all retweets occur around a particular tweet? </b><br></p>
<p>If a tweet has been retweeted, the <i>'retweeted_status'</i>  field gives many interesting details about the original tweet itself and its author. </p>
<p>We can measure a tweet's popularity by analyzing the <b><i>retweet<em>count</em></i></b> and <b><i>favoritecount</i></b> fields. But let's also extract the number of followers of the tweeter  —  we have a lot of celebs in the picture, so <b>can we tell if their advocating for #WeLoveTheEarth influenced a significant proportion of their followers?</b></p>
<hr>
<p><i><b>Note</b>: The retweet_count gives us the total number of times the original tweet was retweeted. It should be the same in both the original tweet and all the next retweets. Tinkering around with some sample tweets and the official documentaiton are the way to get your head around the mnay fields.</i></p>

```python
# Extracting useful information from retweets
retweets = [(tweet['retweet_count'], 
             tweet['retweeted_status']['favorite_count'], 
             tweet['retweeted_status']['user']['followers_count'], 
             tweet['retweeted_status']['user']['screen_name'],
             tweet['text']) for tweet in tweets if 'retweeted_status' in tweet]
```

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_retweets():
    correct_retweets = [
             (tweet['retweet_count'], 
              tweet['retweeted_status']['favorite_count'],
              tweet['retweeted_status']['user']['followers_count'],
              tweet['retweeted_status']['user']['screen_name'],
              tweet['text']) 
            
            for tweet in tweets 
                if 'retweeted_status' in tweet
           ]
    assert correct_retweets == retweets, \
    "The retweets variable does not have the expected values. Check the names of the extracted field and their order."
```

    1/1 tests passed

## 8. A table that speaks a 1000 words
<p>Let's manipulate the data further and visualize it in a better and richer way — <em>"looks matter!"</em></p>

```python
# Importing modules
import matplotlib.pyplot as plt
import pandas as pd

# Create a DataFrame and visualize the data in a pretty and insightful format
df = pd.DataFrame(retweets, 
                  columns=['Retweets',
                           'Favorites',
                           'Followers', 
                           'ScreenName', 
                           'Text']).groupby(['ScreenName',
                                             'Text',
                                             'Followers']).sum().sort_values(by=['Followers'], ascending=False)

df.style.background_gradient()
```

<style  type="text/css" >
    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row0_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row0_col1 {
            background-color:  #fbf4f9;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row1_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row1_col1 {
            background-color:  #fbf4f9;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row2_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row2_col1 {
            background-color:  #fbf4f9;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row3_col0 {
            background-color:  #dedcec;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row3_col1 {
            background-color:  #dedcec;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row4_col0 {
            background-color:  #023858;
            color:  #f1f1f1;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row4_col1 {
            background-color:  #023858;
            color:  #f1f1f1;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row5_col0 {
            background-color:  #f7f0f7;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row5_col1 {
            background-color:  #e3e0ee;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row6_col0 {
            background-color:  #f7f0f7;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row6_col1 {
            background-color:  #e3e0ee;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row7_col0 {
            background-color:  #f9f2f8;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row7_col1 {
            background-color:  #faf2f8;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row8_col0 {
            background-color:  #1278b4;
            color:  #f1f1f1;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row8_col1 {
            background-color:  #529bc7;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row9_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row9_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row10_col0 {
            background-color:  #e3e0ee;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row10_col1 {
            background-color:  #d8d7e9;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row11_col0 {
            background-color:  #0570b0;
            color:  #f1f1f1;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row11_col1 {
            background-color:  #7dacd1;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row12_col0 {
            background-color:  #0567a2;
            color:  #f1f1f1;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row12_col1 {
            background-color:  #6da6cd;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row13_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row13_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row14_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row14_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row15_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row15_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row16_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row16_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row17_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row17_col1 {
            background-color:  #fcf4fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row18_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row18_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row19_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row19_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row20_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row20_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row21_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row21_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row22_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row22_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row23_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row23_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row24_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row24_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row25_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row25_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row26_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row26_col1 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row27_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row27_col1 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row28_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row28_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row29_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row29_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row30_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row30_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row31_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row31_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row32_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row32_col1 {
            background-color:  #fbf4f9;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row33_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row33_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row34_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row34_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row35_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row35_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row36_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row36_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row37_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row37_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row38_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row38_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row39_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row39_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row40_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row40_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row41_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row41_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row42_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row42_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row43_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row43_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row44_col0 {
            background-color:  #fbf3f9;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row44_col1 {
            background-color:  #fcf4fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row45_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row45_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row46_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row46_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row47_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row47_col1 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row48_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row48_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row49_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row49_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row50_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row50_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row51_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row51_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row52_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row52_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row53_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row53_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row54_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row54_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row55_col0 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row55_col1 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row56_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row56_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row57_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row57_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row58_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row58_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row59_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row59_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row60_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row60_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row61_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row61_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row62_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row62_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row63_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row63_col1 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row64_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row64_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row65_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row65_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row66_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row66_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row67_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row67_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row68_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row68_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row69_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row69_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row70_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row70_col1 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row71_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row71_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row72_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row72_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row73_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row73_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row74_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row74_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row75_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row75_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row76_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row76_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row77_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row77_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row78_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row78_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row79_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row79_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row80_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row80_col1 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row81_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row81_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row82_col0 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row82_col1 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row83_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row83_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row84_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row84_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row85_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row85_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row86_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row86_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row87_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row87_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row88_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row88_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row89_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row89_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row90_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row90_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row91_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row91_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row92_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row92_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row93_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row93_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row94_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row94_col1 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row95_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row95_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row96_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row96_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row97_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row97_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row98_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row98_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row99_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row99_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row100_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row100_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row101_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row101_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row102_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row102_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row103_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row103_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row104_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row104_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row105_col0 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row105_col1 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row106_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row106_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row107_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row107_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row108_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row108_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row109_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row109_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row110_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row110_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row111_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row111_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row112_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row112_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row113_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row113_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row114_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row114_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row115_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row115_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row116_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row116_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row117_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row117_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row118_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row118_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row119_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row119_col1 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row120_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row120_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row121_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row121_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row122_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row122_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row123_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row123_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row124_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row124_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row125_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row125_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row126_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row126_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row127_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row127_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row128_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row128_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row129_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row129_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row130_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row130_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row131_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row131_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row132_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row132_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row133_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row133_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row134_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row134_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row135_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row135_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row136_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row136_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row137_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row137_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row138_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row138_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row139_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row139_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row140_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row140_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row141_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row141_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row142_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row142_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row143_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row143_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row144_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row144_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row145_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row145_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row146_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row146_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row147_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row147_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row148_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row148_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row149_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row149_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row150_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row150_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row151_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row151_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row152_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row152_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row153_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row153_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row154_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row154_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row155_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row155_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row156_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row156_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row157_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row157_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row158_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row158_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row159_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row159_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row160_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row160_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row161_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row161_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row162_col0 {
            background-color:  #f7f0f7;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row162_col1 {
            background-color:  #f9f2f8;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row163_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row163_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row164_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row164_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row165_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row165_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row166_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row166_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row167_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row167_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row168_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row168_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row169_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row169_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row170_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row170_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row171_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row171_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row172_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row172_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row173_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row173_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row174_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row174_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row175_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row175_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row176_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row176_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row177_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row177_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row178_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row178_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row179_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row179_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row180_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row180_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row181_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row181_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row182_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row182_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row183_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row183_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row184_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row184_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row185_col0 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row185_col1 {
            background-color:  #fef6fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row186_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row186_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row187_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row187_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row188_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row188_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row189_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row189_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row190_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row190_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row191_col0 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row191_col1 {
            background-color:  #fef6fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row192_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row192_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row193_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row193_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row194_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row194_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row195_col0 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row195_col1 {
            background-color:  #fdf5fa;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row196_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row196_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row197_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row197_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row198_col0 {
            background-color:  #fff7fb;
            color:  #000000;
        }    #T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row198_col1 {
            background-color:  #fff7fb;
            color:  #000000;
        }</style><table id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Retweets</th>        <th class="col_heading level0 col1" >Favorites</th>    </tr>    <tr>        <th class="index_name level0" >ScreenName</th>        <th class="index_name level1" >Text</th>        <th class="index_name level2" >Followers</th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row0" class="row_heading level0 row0" rowspan=2>katyperry</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row0" class="row_heading level1 row0" rowspan=2>RT @katyperry: Sure, the Mueller report is out, but @lildickytweets’ "Earth" but will be too tonight. Don't say I never tried to save the w…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row0" class="row_heading level2 row0" >107195569</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row0_col0" class="data row0 col0" >2338</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row0_col1" class="data row0 col1" >10557</td>
            </tr>
            <tr>
                                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row1" class="row_heading level2 row1" >107195568</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row1_col0" class="data row1 col0" >2338</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row1_col1" class="data row1 col1" >10556</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row2" class="row_heading level0 row2" >TheEllenShow</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row2" class="row_heading level1 row2" >RT @TheEllenShow: .@lildickytweets, @justinbieber, @MileyCyrus, @katyperry, @ArianaGrande and more, all in one music video. My head might e…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row2" class="row_heading level2 row2" >77474826</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row2_col0" class="data row2 col0" >2432</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row2_col1" class="data row2 col1" >10086</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row3" class="row_heading level0 row3" rowspan=2>LeoDiCaprio</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row3" class="row_heading level1 row3" >RT @LeoDiCaprio: The @dicapriofdn partners that will benefit from this collaboration include @SharkRayFund, @SolutionsProj, @GreengrantsFun…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row3" class="row_heading level2 row3" >18988898</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row3_col0" class="data row3 col0" >28505</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row3_col1" class="data row3 col1" >78137</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row4" class="row_heading level1 row4" >RT @LeoDiCaprio: Thank you to @lildickytweets and all the artists that came together to make this happen. Net profits from the song, video,…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row4" class="row_heading level2 row4" >18988898</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row4_col0" class="data row4 col0" >149992</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row4_col1" class="data row4 col1" >416018</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row5" class="row_heading level0 row5" rowspan=2>halsey</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row5" class="row_heading level1 row5" rowspan=2>RT @halsey: 🐯🐯🐯 meeeeeeeow 👅 #WeLoveTheEarth https://t.co/JJr6vmKG7U</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row5" class="row_heading level2 row5" >10564842</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row5_col0" class="data row5 col0" >7742</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row5_col1" class="data row5 col1" >69684</td>
            </tr>
            <tr>
                                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row6" class="row_heading level2 row6" >10564841</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row6_col0" class="data row6 col0" >7742</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row6_col1" class="data row6 col1" >69682</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row7" class="row_heading level0 row7" >scooterbraun</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row7" class="row_heading level1 row7" >RT @scooterbraun: Watch #EARTH NOW! #WeLoveTheEarth — https://t.co/OtRfIgcSZL</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row7" class="row_heading level2 row7" >3885179</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row7_col0" class="data row7 col0" >5925</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row7_col1" class="data row7 col1" >14635</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row8" class="row_heading level0 row8" >Spotify</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row8" class="row_heading level1 row8" >RT @Spotify: This is epic. @lildickytweets got @justinbieber, @arianagrande, @halsey, @sanbenito, @edsheeran, @SnoopDogg, @ShawnMendes, @Kr…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row8" class="row_heading level2 row8" >2973277</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row8_col0" class="data row8 col0" >107222</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row8_col1" class="data row8 col1" >237259</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row9" class="row_heading level0 row9" >TomHall</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row9" class="row_heading level1 row9" >RT @TomHall: 🐆

Look Out!

🐆

#Cheetah @LeoDiCaprio  #FridayFeeling #WeLoveTheEarth 

https://t.co/w1O1NyTbwX</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row9" class="row_heading level2 row9" >590841</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row9_col0" class="data row9 col0" >82</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row9_col1" class="data row9 col1" >252</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row10" class="row_heading level0 row10" rowspan=3>lildickytweets</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row10" class="row_heading level1 row10" >RT @lildickytweets: Earth. 4/18 at 9PM PST. #WeLoveTheEarth pre-save link in my bio https://t.co/7HD2xlSFYQ</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row10" class="row_heading level2 row10" >503112</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row10_col0" class="data row10 col0" >25098</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row10_col1" class="data row10 col1" >90974</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row11" class="row_heading level1 row11" rowspan=2>RT @lildickytweets: 🌎 out now #WeLoveTheEarth https://t.co/L22XsoT5P1</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row11" class="row_heading level2 row11" >503112</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row11_col0" class="data row11 col0" >112230</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row11_col1" class="data row11 col1" >199773</td>
            </tr>
            <tr>
                                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row12" class="row_heading level2 row12" >503111</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row12_col0" class="data row12 col0" >119712</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row12_col1" class="data row12 col1" >213072</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row13" class="row_heading level0 row13" >greenpeacefr</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row13" class="row_heading level1 row13" >RT @greenpeacefr: Happening NOW in France : today, to show how much #WeLoveTheEarth, more than 2000 citizens are blocking the headquarters…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row13" class="row_heading level2 row13" >420789</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row13_col0" class="data row13 col0" >128</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row13_col1" class="data row13 col1" >192</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row14" class="row_heading level0 row14" >rlthingy</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row14" class="row_heading level1 row14" >RT @rlthingy: /rlt/ YO GUYS LISTEN TO THIS SONGGGGG #WeLoveTheEarth https://t.co/trUgRG7QBH</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row14" class="row_heading level2 row14" >225977</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row14_col0" class="data row14 col0" >11</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row14_col1" class="data row14 col1" >23</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row15" class="row_heading level0 row15" >SB_Projects</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row15" class="row_heading level1 row15" >RT @SB_Projects: #WeLoveTheEarth out now with @lildickytweets, @justinbieber, @ArianaGrande, @zacbrownband, and 25+ of your other faves htt…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row15" class="row_heading level2 row15" >98418</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row15_col0" class="data row15 col0" >271</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row15_col1" class="data row15 col1" >730</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row16" class="row_heading level0 row16" >biebernovidade</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row16" class="row_heading level1 row16" >RT @biebernovidade: Rio de Janeiro: PRESENTE! #WeLoveTheEarth https://t.co/IJrypKqzSf</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row16" class="row_heading level2 row16" >83281</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row16_col0" class="data row16 col0" >651</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row16_col1" class="data row16 col1" >1499</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row17" class="row_heading level0 row17" >MendesCrewInfo</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row17" class="row_heading level1 row17" >RT @MendesCrewInfo: .@ShawnMendes represents rhinos in the ‘Earth’ music video and feature. His line, “We’re just some rhinos, horny as hec…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row17" class="row_heading level2 row17" >61015</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row17_col0" class="data row17 col0" >2815</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row17_col1" class="data row17 col1" >9599</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row18" class="row_heading level0 row18" rowspan=4>shawnxniallx</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row18" class="row_heading level1 row18" >RT @shawnxniallx: La gente piensa que el calentamiento global no es real, ya abran los ojos y actuemos de una manera real, dime ¿qué te cue…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row18" class="row_heading level2 row18" >53713</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row18_col0" class="data row18 col0" >812</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row18_col1" class="data row18 col1" >1254</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row19" class="row_heading level1 row19" >RT @shawnxniallx: La humanidad es un asco y nunca me cansaré de decirlos ¿no creen que es momento de cambiar? Salvemos nuestro planeta, sal…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row19" class="row_heading level2 row19" >53713</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row19_col0" class="data row19 col0" >604</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row19_col1" class="data row19 col1" >1034</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row20" class="row_heading level1 row20" >RT @shawnxniallx: Vengo a recomendarles a todos esta miniserie que realizó Netflix, en la cual nos muestra cada parte de las especies, lo q…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row20" class="row_heading level2 row20" >53713</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row20_col0" class="data row20 col0" >138</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row20_col1" class="data row20 col1" >299</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row21" class="row_heading level1 row21" >RT @shawnxniallx: Espero que con este video se pueda crear un poco más de conciencia propia, simeplemnte estamos acabando con nuestro plane…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row21" class="row_heading level2 row21" >53713</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row21_col0" class="data row21 col0" >300</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row21_col1" class="data row21 col1" >494</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row22" class="row_heading level0 row22" rowspan=5>SMendesQandA</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row22" class="row_heading level1 row22" >RT @SMendesQandA: #WeLoveTheEarth https://t.co/KDIKYVHFWU</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row22" class="row_heading level2 row22" >53282</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row22_col0" class="data row22 col0" >56</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row22_col1" class="data row22 col1" >339</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row23" class="row_heading level1 row23" >RT @SMendesQandA: Let’s help save the Earth. We’re the ones with the power of change. 🌍  #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row23" class="row_heading level2 row23" >53282</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row23_col0" class="data row23 col0" >122</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row23_col1" class="data row23 col1" >343</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row24" class="row_heading level1 row24" >RT @SMendesQandA: So you can basically say you have a song with many of the artists we have asked you to collaborate with...smart move mend…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row24" class="row_heading level2 row24" >53282</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row24_col0" class="data row24 col0" >116</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row24_col1" class="data row24 col1" >717</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row25" class="row_heading level1 row25" >RT @SMendesQandA: “We’re just some rhinos, horny as heck” — Shawn’s part on #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row25" class="row_heading level2 row25" >53282</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row25_col0" class="data row25 col0" >244</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row25_col1" class="data row25 col1" >1420</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row26" class="row_heading level1 row26" >RT @SMendesQandA: “We’re just some rhinos horny as heck” — Shawn Mendes #WeLoveTheEarth https://t.co/URnHb0DTWN</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row26" class="row_heading level2 row26" >53282</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row26_col0" class="data row26 col0" >768</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row26_col1" class="data row26 col1" >3309</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row27" class="row_heading level0 row27" >ShawnUpdatesSA</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row27" class="row_heading level1 row27" >RT @ShawnUpdatesSA: Shawn Mendes: rinocerontes.
#WeLoveTheEarth

'La población de rinocerontes negros está casi extinta, y las otras cuatro…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row27" class="row_heading level2 row27" >52424</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row27_col0" class="data row27 col0" >850</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row27_col1" class="data row27 col1" >1807</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row28" class="row_heading level0 row28" >gtbriel</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row28" class="row_heading level1 row28" >RT @gtbriel: vimos o cu do justin bieber

logo em seguida a ariana sair do cu do justin 

e logo em seguuda a ariana sendo morta pela halse…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row28" class="row_heading level2 row28" >49215</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row28_col0" class="data row28 col0" >581</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row28_col1" class="data row28 col1" >970</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row29" class="row_heading level0 row29" >MileySmilerNews</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row29" class="row_heading level1 row29" >RT @MileySmilerNews: Miley’s cameo in the Earth song is so cute #WeLoveTheEarth https://t.co/Byk9rkhMpG</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row29" class="row_heading level2 row29" >47840</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row29_col0" class="data row29 col0" >15</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row29_col1" class="data row29 col1" >116</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row30" class="row_heading level0 row30" >ArianatorFallen</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row30" class="row_heading level1 row30" >RT @ArianatorFallen: Ariana vocals had saved the earth . This song is so important #WeLoveTheEarth https://t.co/Lg9jsPRD5z</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row30" class="row_heading level2 row30" >44426</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row30_col0" class="data row30 col0" >84</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row30_col1" class="data row30 col1" >258</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row31" class="row_heading level0 row31" rowspan=2>MendesNotified</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row31" class="row_heading level1 row31" >RT @MendesNotified: Rhinos - Shawn Mendes🦏🖤
“The black rhino population is nearly extinct, and the four other species of rhinos found in Af…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row31" class="row_heading level2 row31" >39726</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row31_col0" class="data row31 col0" >258</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row31_col1" class="data row31 col1" >858</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row32" class="row_heading level1 row32" >RT @MendesNotified: shawn reading his line for the song #WeLoveTheEarth:  https://t.co/dcWJFDlVMd</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row32" class="row_heading level2 row32" >39726</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row32_col0" class="data row32 col0" >2465</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row32_col1" class="data row32 col1" >10475</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row33" class="row_heading level0 row33" >badweputation</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row33" class="row_heading level1 row33" >RT @badweputation: n adianta vcs comentarem sobre a importância da preservação hj e amanhã já esquecerem e tbm lembrando q o atual presiden…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row33" class="row_heading level2 row33" >38787</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row33_col0" class="data row33 col0" >119</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row33_col1" class="data row33 col1" >183</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row34" class="row_heading level0 row34" rowspan=2>isbreakls</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row34" class="row_heading level1 row34" >RT @isbreakls: Queria dizer que na música do Lil Dicky tem 28 artistas incríveis mais quem eu amo mesmo é um babuíno chamado Justin Bieber.…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row34" class="row_heading level2 row34" >37473</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row34_col0" class="data row34 col0" >95</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row34_col1" class="data row34 col1" >215</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row35" class="row_heading level1 row35" >RT @isbreakls: A música e o clipe tá incrível vamos espalhar o verdadeiro motivo da música que é fazer com que as pessoas pensem nos seus a…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row35" class="row_heading level2 row35" >37473</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row35_col0" class="data row35 col0" >684</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row35_col1" class="data row35 col1" >1068</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row36" class="row_heading level0 row36" >NoticiasSmilers</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row36" class="row_heading level1 row36" >RT @NoticiasSmilers: Soy un elefante, tengo basura en mi trompa. -Pequeño cameo de Miley en la canción Earth de Lil Dicky- #WeLoveTheEarth…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row36" class="row_heading level2 row36" >32649</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row36_col0" class="data row36 col0" >7</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row36_col1" class="data row36 col1" >4</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row37" class="row_heading level0 row37" >ThrowbacksBTS</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row37" class="row_heading level1 row37" >RT @ThrowbacksBTS: Friendly reminder to use less plastic, recycle and contribute in some way to benefit humanity. The world is dying we nee…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row37" class="row_heading level2 row37" >32498</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row37_col0" class="data row37 col0" >370</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row37_col1" class="data row37 col1" >816</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row38" class="row_heading level0 row38" >btsargento</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row38" class="row_heading level1 row38" >RT @btsargento: ▪ estas son varias cosas que podemos hacer para construir un planeta mejor, sin contaminación y un lugar donde todos aporte…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row38" class="row_heading level2 row38" >31453</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row38_col0" class="data row38 col0" >67</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row38_col1" class="data row38 col1" >143</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row39" class="row_heading level0 row39" >biebersmaniabrs</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row39" class="row_heading level1 row39" >RT @biebersmaniabrs: SAIU! Ouçam e assistam “Earth”, música de Lil Dicky com Justin Bieber e mais 29 artistas. 🌏🎶

Video: https://t.co/oHRR…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row39" class="row_heading level2 row39" >26097</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row39_col0" class="data row39 col0" >341</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row39_col1" class="data row39 col1" >463</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row40" class="row_heading level0 row40" >landsrauhl</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row40" class="row_heading level1 row40" >RT @landsrauhl: I loved what lil dicky did. There’s so many popular artists on the track which hopefully means more of a variety of people…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row40" class="row_heading level2 row40" >25071</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row40_col0" class="data row40 col0" >128</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row40_col1" class="data row40 col1" >306</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row41" class="row_heading level0 row41" >biebsrell</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row41" class="row_heading level1 row41" >RT @biebsrell: J: ¿Vamos a morir?
L: ¿Sabes qué, Bieber? Podríamos morir. No voy a mentirte. Quiero decir, hay mucha gente ahí afuera que n…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row41" class="row_heading level2 row41" >23301</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row41_col0" class="data row41 col0" >730</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row41_col1" class="data row41 col1" >1344</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row42" class="row_heading level0 row42" rowspan=3>ShawnNewsPoland</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row42" class="row_heading level1 row42" >RT @ShawnNewsPoland: “We’re just some rhinos, horny as heck” — Shawna tekst w piosence #WeLoveTheEarth https://t.co/NsOmYfoe7u</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row42" class="row_heading level2 row42" >22067</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row42_col0" class="data row42 col0" >97</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row42_col1" class="data row42 col1" >523</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row43" class="row_heading level1 row43" >RT @ShawnNewsPoland: Wyjaśnienie tekstu Shawna #WeLoveTheEarth https://t.co/NiShcC8WGW</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row43" class="row_heading level2 row43" >22067</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row43_col0" class="data row43 col0" >105</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row43_col1" class="data row43 col1" >440</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row44" class="row_heading level1 row44" >RT @ShawnNewsPoland: Słuchajcie wszędzie gdzie się da! #WeLoveTheEarth dochód z piosenki zostanie przekazany fundacji założonej przez DiCap…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row44" class="row_heading level2 row44" >22067</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row44_col0" class="data row44 col0" >4410</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row44_col1" class="data row44 col1" >8720</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row45" class="row_heading level0 row45" >NLiddle16</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row45" class="row_heading level1 row45" >RT @NLiddle16: #Earth isn’t supposed to break records or chart. This song is to bring awareness. We have to change now. We have to love mor…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row45" class="row_heading level2 row45" >21180</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row45_col0" class="data row45 col0" >27</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row45_col1" class="data row45 col1" >134</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row46" class="row_heading level0 row46" >ArianaRenewsFR</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row46" class="row_heading level1 row46" >RT @ArianaRenewsFR: #WeLoveTheEarth est maintenant disponible sur toutes les plateformes ! 

YouTube : https://t.co/zSpCdE74lV

iTunes : ht…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row46" class="row_heading level2 row46" >20794</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row46_col0" class="data row46 col0" >5</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row46_col1" class="data row46 col1" >20</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row47" class="row_heading level0 row47" >iBeliebersMx</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row47" class="row_heading level1 row47" >RT @iBeliebersMx: Justin: ¿Vamos a morir?

Lil Dicky: "Sabes Bieber... podemos morir. No te voy a mentir a ti, hay muchas personas que pien…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row47" class="row_heading level2 row47" >19745</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row47_col0" class="data row47 col0" >2236</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row47_col1" class="data row47 col1" >3872</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row48" class="row_heading level0 row48" >JBCrewdotcom</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row48" class="row_heading level1 row48" >RT @JBCrewdotcom: #WeLoveTheEarth Merchandise available to purchase with proceeds going to The Leonardo DiCaprio Foundation dedicated to th…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row48" class="row_heading level2 row48" >17812</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row48_col0" class="data row48 col0" >89</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row48_col1" class="data row48 col1" >186</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row49" class="row_heading level0 row49" >dimplecabello</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row49" class="row_heading level1 row49" >RT @dimplecabello: “¿Que vamos a defender? El amor. Y nosotros amamos la tierra.” Este video es precioso, últimamente estamos dañando tanto…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row49" class="row_heading level2 row49" >17590</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row49_col0" class="data row49 col0" >286</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row49_col1" class="data row49 col1" >445</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row50" class="row_heading level0 row50" >TeamAGPoland</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row50" class="row_heading level1 row50" >RT @TeamAGPoland: Utwór "Earth" jest już dostępny! Ariana wcieliła się w postać zebry, a cały dochód ze sprzedaży utworu zostanie przekazan…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row50" class="row_heading level2 row50" >17157</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row50_col0" class="data row50 col0" >44</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row50_col1" class="data row50 col1" >142</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row51" class="row_heading level0 row51" >bieberpakiss</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row51" class="row_heading level1 row51" >RT @bieberpakiss: HI IM A BABOON IM LIKE A MAN JUST LESS ADVANCED AND MY ANUS IS HUGE #WeLoveTheEarth https://t.co/tqhfvv7PKf</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row51" class="row_heading level2 row51" >16288</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row51_col0" class="data row51 col0" >148</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row51_col1" class="data row51 col1" >286</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row52" class="row_heading level0 row52" >yourbiebernews</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row52" class="row_heading level1 row52" >RT @yourbiebernews: Justin Bieber: Baboon

#WeLoveTheEarth https://t.co/dlvl1M28Mg</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row52" class="row_heading level2 row52" >14121</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row52_col0" class="data row52 col0" >198</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row52_col1" class="data row52 col1" >404</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row53" class="row_heading level0 row53" >bizzleslovej</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row53" class="row_heading level1 row53" >RT @bizzleslovej: Parliamo di Leo DiCaprio che entra in scena sulla nave del Titanic stile Jack #WeLoveTheEarth https://t.co/VxZscAiOhZ</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row53" class="row_heading level2 row53" >13151</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row53_col0" class="data row53 col0" >5</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row53_col1" class="data row53 col1" >8</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row54" class="row_heading level0 row54" >holdtightlive</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row54" class="row_heading level1 row54" >RT @holdtightlive: THIS SONG IS SO BEAUTIFUL THE VIDEO IS ABSOLUTELY AMAZING AND IT’S FOR A GOOD CAUSE SO LETS GOOO STREAM IT BUY IT WATCH…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row54" class="row_heading level2 row54" >10331</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row54_col0" class="data row54 col0" >35</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row54_col1" class="data row54 col1" >83</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row55" class="row_heading level0 row55" >needyellie</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row55" class="row_heading level1 row55" >RT @needyellie: please keep steaming this song, all proceeds go to an extremely important cause. save planet earth!!
#WeLoveTheEarth https:…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row55" class="row_heading level2 row55" >10319</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row55_col0" class="data row55 col0" >1240</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row55_col1" class="data row55 col1" >2884</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row56" class="row_heading level0 row56" >gladwithmyidols</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row56" class="row_heading level1 row56" >RT @gladwithmyidols: So... Halsey killed Ariana #WeLoveTheEarth https://t.co/Qquu4YfgzE</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row56" class="row_heading level2 row56" >9987</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row56_col0" class="data row56 col0" >23</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row56_col1" class="data row56 col1" >91</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row57" class="row_heading level0 row57" >TJOfficial_</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row57" class="row_heading level1 row57" >RT @TJOfficial_: We love the earth it is our planet 🌍 🎶 #WeLoveTheEarth It’s so beautiful.</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row57" class="row_heading level2 row57" >9693</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row57_col0" class="data row57 col0" >6</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row57_col1" class="data row57 col1" >12</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row58" class="row_heading level0 row58" rowspan=2>MCyrus__forever</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row58" class="row_heading level1 row58" >RT @MCyrus__forever: Cały dochód z tej piosenki trafi do fundacji Leonardo DiCaprio, poświęconej ochronie i dobrobytowi wszystkich mieszkań…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row58" class="row_heading level2 row58" >9680</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row58_col0" class="data row58 col0" >46</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row58_col1" class="data row58 col1" >79</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row59" class="row_heading level1 row59" >RT @MCyrus__forever: Ten teledysk jest świetny, a piosenka ma naprawdę bardzo ważne przesłanie 🌎🌱 #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row59" class="row_heading level2 row59" >9680</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row59_col0" class="data row59 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row59_col1" class="data row59 col1" >5</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row60" class="row_heading level0 row60" >justinxrespect</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row60" class="row_heading level1 row60" >RT @justinxrespect: “are we gonna die” ay loco. #WeLoveTheEarth https://t.co/zwof29P4Uw</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row60" class="row_heading level2 row60" >9257</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row60_col0" class="data row60 col0" >9</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row60_col1" class="data row60 col1" >21</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row61" class="row_heading level0 row61" rowspan=2>cyruseyes_</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row61" class="row_heading level1 row61" >RT @cyruseyes_: Qui non stiamo parlando abbastanza di Leonardo DiCaprio e di questa scena 
#WeLoveTheEarth https://t.co/zUfOWBy7ct</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row61" class="row_heading level2 row61" >9148</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row61_col0" class="data row61 col0" >22</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row61_col1" class="data row61 col1" >148</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row62" class="row_heading level1 row62" >RT @cyruseyes_: Questo video deve diventare un film. Il messaggio arriverebbe veramente a tutti. @ Disney sai cosa fare 
#WeLoveTheEarth ht…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row62" class="row_heading level2 row62" >9148</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row62_col0" class="data row62 col0" >10</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row62_col1" class="data row62 col1" >52</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row63" class="row_heading level0 row63" >ChartBTS</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row63" class="row_heading level1 row63" >RT @ChartBTS: "We love the earth it is our planet  
We love the earth it is our home" 

ARMYs, support this important cause, it is our home…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row63" class="row_heading level2 row63" >8527</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row63_col0" class="data row63 col0" >705</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row63_col1" class="data row63 col1" >1731</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row64" class="row_heading level0 row64" >MileyDimension</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row64" class="row_heading level1 row64" >RT @MileyDimension: I think everyone should see this! 
It is about time to do something. #WeLoveTheEarth 
https://t.co/WmMDhsBq19</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row64" class="row_heading level2 row64" >7745</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row64_col0" class="data row64 col0" >645</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row64_col1" class="data row64 col1" >969</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row65" class="row_heading level0 row65" >cabeyoomoon</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row65" class="row_heading level1 row65" >RT @cabeyoomoon: Ta piosenka to bop,  wpada w ucho  i dochody z niej idą na dobry cel,  warto słuchać w kółko i w kółko gdziekolwiek się ty…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row65" class="row_heading level2 row65" >7732</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row65_col0" class="data row65 col0" >9</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row65_col1" class="data row65 col1" >23</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row66" class="row_heading level0 row66" >stonyproud</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row66" class="row_heading level1 row66" >RT @stonyproud: agora que percebi que o clipe todo foi no cu do Justin pqp que cu arrombado  #WeLoveTheEarth https://t.co/I2edu6J9be</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row66" class="row_heading level2 row66" >7728</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row66_col0" class="data row66 col0" >49</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row66_col1" class="data row66 col1" >115</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row67" class="row_heading level0 row67" >hoe4exhoee</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row67" class="row_heading level1 row67" >RT @hoe4exhoee: Lil Dicky - Earth (Official Music Video) https://t.co/XT4xdm9XoN  

KRIS WU's PART IS ON 5:43. It is short but I'm so glad…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row67" class="row_heading level2 row67" >6870</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row67_col0" class="data row67 col0" >10</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row67_col1" class="data row67 col1" >8</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row68" class="row_heading level0 row68" >KCUnidosBR</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row68" class="row_heading level1 row68" >RT @KCUnidosBR: Quem diria em KatyCats? 2 músicas no mesmo dia #ConCalmaRemix #WeLoveTheEarth https://t.co/FF7Be15lhz</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row68" class="row_heading level2 row68" >6458</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row68_col0" class="data row68 col0" >59</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row68_col1" class="data row68 col1" >96</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row69" class="row_heading level0 row69" >Ari_grandeJP</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row69" class="row_heading level1 row69" >RT @Ari_grandeJP: . @lildickytweets の
新曲 #EARTH が公開されました💙🌏

アリアナはシマウマとして参加してます！👀💗✨

 #WeLoveTheEarth https://t.co/5g1clvAZoO</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row69" class="row_heading level2 row69" >6141</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row69_col0" class="data row69 col0" >44</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row69_col1" class="data row69 col1" >306</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row70" class="row_heading level0 row70" >becauseihadyou</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row70" class="row_heading level1 row70" >RT @becauseihadyou: Don’t know why people are being nasty about ‘Earth’. It’s not a song meant to chart or break records, it’s to raise awa…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row70" class="row_heading level2 row70" >5647</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row70_col0" class="data row70 col0" >2484</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row70_col1" class="data row70 col1" >6444</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row71" class="row_heading level0 row71" rowspan=2>biebersmybro</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row71" class="row_heading level1 row71" >RT @biebersmybro: beliebers are promoting the song the hardest lol wbk we are the best fandom ever #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row71" class="row_heading level2 row71" >5314</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row71_col0" class="data row71 col0" >14</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row71_col1" class="data row71 col1" >49</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row72" class="row_heading level1 row72" >RT @biebersmybro: WE FINALLY HEARD JUSTIN AND ARIANA IN ONE SONG #WeLoveTheEarth https://t.co/RqHTRButmx</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row72" class="row_heading level2 row72" >5314</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row72_col0" class="data row72 col0" >350</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row72_col1" class="data row72 col1" >996</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row73" class="row_heading level0 row73" >imagiwation</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row73" class="row_heading level1 row73" >RT @imagiwation: entre tanta coisa ruim e tóxica que tá tendo ultimamente a gente tem a chance de se unir por uma causa boa, então não vamo…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row73" class="row_heading level2 row73" >5208</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row73_col0" class="data row73 col0" >88</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row73_col1" class="data row73 col1" >129</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row74" class="row_heading level0 row74" rowspan=2>triedsadlonel</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row74" class="row_heading level1 row74" >RT @triedsadlonel: piosenka mega mi sie podoba,taka fajna wesoła(pod katem melodii) natomiast calosc mnie hitnela mocno,bo to serio jest pr…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row74" class="row_heading level2 row74" >4941</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row74_col0" class="data row74 col0" >10</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row74_col1" class="data row74 col1" >34</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row75" class="row_heading level1 row75" >RT @triedsadlonel: kiedy kazdy byl przekonany ze Shawn bedzie żyrafa a tu jeb nosorożcem #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row75" class="row_heading level2 row75" >4941</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row75_col0" class="data row75 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row75_col1" class="data row75 col1" >10</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row76" class="row_heading level0 row76" >neznayuchtotut</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row76" class="row_heading level1 row76" >RT @neznayuchtotut: вау, так много артистов объединились, чтобы поднять насущную проблему нашей планеты о том, что ее нужно защищать и люби…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row76" class="row_heading level2 row76" >4621</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row76_col0" class="data row76 col0" >8</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row76_col1" class="data row76 col1" >150</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row77" class="row_heading level0 row77" >demisfakesmile</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row77" class="row_heading level1 row77" >RT @demisfakesmile: stream. stream. stream this song. its for a good cause, let’s save the earth 🌍 💙💚 #WeLoveTheEarth https://t.co/vgABUfce…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row77" class="row_heading level2 row77" >4421</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row77_col0" class="data row77 col0" >504</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row77_col1" class="data row77 col1" >984</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row78" class="row_heading level0 row78" >SoundOfSeries</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row78" class="row_heading level1 row78" >RT @SoundOfSeries: #INFOSOS : 
'WeLoveTheEarth' est disponible sur YouTube. Le but de cette chanson n’est pas de devenir le tube de l’été,…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row78" class="row_heading level2 row78" >4393</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row78_col0" class="data row78 col0" >80</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row78_col1" class="data row78 col1" >72</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row79" class="row_heading level0 row79" >carawcciolo</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row79" class="row_heading level1 row79" >RT @carawcciolo: Halsey zjada Ariane na śniadanie (koloryzowane) 😅 #WeLoveTheEarth https://t.co/FV4MZSOXlu</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row79" class="row_heading level2 row79" >4246</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row79_col0" class="data row79 col0" >63</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row79_col1" class="data row79 col1" >194</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row80" class="row_heading level0 row80" rowspan=2>gcldendays</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row80" class="row_heading level1 row80" >RT @gcldendays: Be careful who you call ugly in middle school 😉
#WeLoveTheEarth https://t.co/4jvr8Xn397</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row80" class="row_heading level2 row80" >4122</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row80_col0" class="data row80 col0" >394</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row80_col1" class="data row80 col1" >1698</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row81" class="row_heading level1 row81" >RT @gcldendays: No one: 
Not even a soul:

Me:
#WeLoveTheEarth https://t.co/i4BxsXBwny</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row81" class="row_heading level2 row81" >4122</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row81_col0" class="data row81 col0" >408</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row81_col1" class="data row81 col1" >1189</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row82" class="row_heading level0 row82" rowspan=2>biebercentineo</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row82" class="row_heading level1 row82" >RT @biebercentineo: Justin : are we gonna die? 
Lil dicky: you know bieber we might die 

BTCH IM CRYING #EARTH #WeLoveTheEarth #WELOVEEART…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row82" class="row_heading level2 row82" >4038</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row82_col0" class="data row82 col0" >1551</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row82_col1" class="data row82 col1" >3555</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row83" class="row_heading level1 row83" >RT @biebercentineo: THIS SONG IS SO GOOD 😭 #EARTH  #WeLoveTheEarth https://t.co/3hM7ZU2eYh</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row83" class="row_heading level2 row83" >4038</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row83_col0" class="data row83 col0" >79</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row83_col1" class="data row83 col1" >215</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row84" class="row_heading level0 row84" >Bizzbiebsz</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row84" class="row_heading level1 row84" >RT @Bizzbiebsz: So after so many years we finally got Justin x Arina collab and they even gave us zebra and baboon

Stream #WeloveTheEarth…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row84" class="row_heading level2 row84" >3889</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row84_col0" class="data row84 col0" >297</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row84_col1" class="data row84 col1" >879</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row85" class="row_heading level0 row85" >jvkejams</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row85" class="row_heading level1 row85" >RT @jvkejams: I feel like the song will showcase the animals in a very comedic way (bc its how most lil dicky’s songs are) to raise awarene…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row85" class="row_heading level2 row85" >3861</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row85_col0" class="data row85 col0" >20</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row85_col1" class="data row85 col1" >104</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row86" class="row_heading level0 row86" >larryxcolours</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row86" class="row_heading level1 row86" >RT @larryxcolours: ¿Cómo pueden ayudar a la organización? 
-Compren la mercancia, las ganancias irán directamente para ayudar a la tierra.…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row86" class="row_heading level2 row86" >3766</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row86_col0" class="data row86 col0" >330</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row86_col1" class="data row86 col1" >612</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row87" class="row_heading level0 row87" >sitevolts</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row87" class="row_heading level1 row87" >RT @sitevolts: CROSSOVER MAIOR QUE VINGADORES 😵 Justin Bieber, Ariana Grande, Katy Perry, Halsey, Sia, Ed Sheeran, Meghan Trainor e Miley C…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row87" class="row_heading level2 row87" >3707</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row87_col0" class="data row87 col0" >130</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row87_col1" class="data row87 col1" >366</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row88" class="row_heading level0 row88" >JDBieberPol</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row88" class="row_heading level1 row88" >RT @JDBieberPol: Gwiazdy jako zwierzęta w teledysku #Earth #WeLoveTheEarth https://t.co/3aA4mE56Y3</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row88" class="row_heading level2 row88" >3475</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row88_col0" class="data row88 col0" >34</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row88_col1" class="data row88 col1" >99</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row89" class="row_heading level0 row89" rowspan=2>nervous_taste</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row89" class="row_heading level1 row89" >RT @nervous_taste: Have u thought that we will have:

SHAWN MENDES FT ARIANA GRANDE 
SHAWN MENDES FT JUSTIN BIEBER 
SHAWN MENDES FT HALSEY…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row89" class="row_heading level2 row89" >3283</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row89_col0" class="data row89 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row89_col1" class="data row89 col1" >9</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row90" class="row_heading level1 row90" >RT @nervous_taste: Shawn isn’t the giraffe 

#WeLoveTheEarth https://t.co/0PJdZnkP87</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row90" class="row_heading level2 row90" >3283</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row90_col0" class="data row90 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row90_col1" class="data row90 col1" >0</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row91" class="row_heading level0 row91" >nopromisesv</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row91" class="row_heading level1 row91" >RT @nopromisesv: A ogólnie sam teledysk jest świetny, nie spodziewałam się tego #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row91" class="row_heading level2 row91" >3283</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row91_col0" class="data row91 col0" >7</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row91_col1" class="data row91 col1" >77</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row92" class="row_heading level0 row92" >INLOVEWITHDS</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row92" class="row_heading level1 row92" >RT @INLOVEWITHDS: Questo video è semplicemente spettacolare e il messaggio che vuole trasmettere è bellissimo
wow non ho parole
Tutti gli a…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row92" class="row_heading level2 row92" >3153</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row92_col0" class="data row92 col0" >14</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row92_col1" class="data row92 col1" >49</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row93" class="row_heading level0 row93" >agbkissy</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row93" class="row_heading level1 row93" >RT @agbkissy: all of yall saying earth is a bad song are immature... its not supposed to be the next big hit, it was made to spread awarene…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row93" class="row_heading level2 row93" >3098</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row93_col0" class="data row93 col0" >584</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row93_col1" class="data row93 col1" >1356</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row94" class="row_heading level0 row94" rowspan=2>dreamsiinflate</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row94" class="row_heading level1 row94" >RT @dreamsiinflate: #WeLoveTheEarth “i am a fat fucking pig” okay brendon urie https://t.co/FdJmq31xZc</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row94" class="row_heading level2 row94" >3045</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row94_col0" class="data row94 col0" >1107</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row94_col1" class="data row94 col1" >3426</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row95" class="row_heading level1 row95" >RT @dreamsiinflate: #WeLoveTheEarth they are all these informative cards on the website which are pretty cool https://t.co/qq0GWJ0q0G</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row95" class="row_heading level2 row95" >3045</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row95_col0" class="data row95 col0" >208</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row95_col1" class="data row95 col1" >840</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row96" class="row_heading level0 row96" >SMendesMedia</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row96" class="row_heading level1 row96" >RT @SMendesMedia: . @ShawnMendes’ part on l “Earth” 🌎 

#WeLoveTheEarth (@lildickytweets)
• https://t.co/XrpJbZ6zY7 https://t.co/o2dO7V5cz4</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row96" class="row_heading level2 row96" >2815</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row96_col0" class="data row96 col0" >238</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row96_col1" class="data row96 col1" >1120</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row97" class="row_heading level0 row97" rowspan=2>kyzztin</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row97" class="row_heading level1 row97" >RT @kyzztin: The whole concept of this is super dope. lil dicky really got so many huge artists to be part of this amazing project and give…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row97" class="row_heading level2 row97" >2641</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row97_col0" class="data row97 col0" >21</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row97_col1" class="data row97 col1" >79</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row98" class="row_heading level1 row98" >RT @kyzztin: same energy #WeloveTheEarth https://t.co/YfTTS6BRiC</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row98" class="row_heading level2 row98" >2641</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row98_col0" class="data row98 col0" >10</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row98_col1" class="data row98 col1" >27</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row99" class="row_heading level0 row99" rowspan=2>xKittyMendes</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row99" class="row_heading level1 row99" >RT @xKittyMendes: SHAWN JEST NOSOROŻCEM
Jego od razu poznałam, bo z innymi miałam problem XD #WeLoveTheEarth https://t.co/21ICMTDdmn</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row99" class="row_heading level2 row99" >2597</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row99_col0" class="data row99 col0" >48</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row99_col1" class="data row99 col1" >426</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row100" class="row_heading level1 row100" >RT @xKittyMendes: Nie sądziłam, że potrzebuję usłyszeć z ust Shawna słowa horny XDD #WeLoveTheEarth https://t.co/TkMA07iNj5</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row100" class="row_heading level2 row100" >2597</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row100_col0" class="data row100 col0" >326</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row100_col1" class="data row100 col1" >1074</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row101" class="row_heading level0 row101" rowspan=2>kajagafelgaja</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row101" class="row_heading level1 row101" >RT @kajagafelgaja: macie tu moją przemowe #WeLoveTheEarth https://t.co/1KKrPIRllX</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row101" class="row_heading level2 row101" >2526</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row101_col0" class="data row101 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row101_col1" class="data row101 col1" >0</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row102" class="row_heading level1 row102" >RT @kajagafelgaja: czy to Was nie dociera że ta piosenka nie ma być dobra, tylko prosta, trafiająca do wszystkich i wpadająca w ucho? i moż…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row102" class="row_heading level2 row102" >2526</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row102_col0" class="data row102 col0" >30</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row102_col1" class="data row102 col1" >32</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row103" class="row_heading level0 row103" >luvmyburito</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row103" class="row_heading level1 row103" >RT @luvmyburito: głosy ariany i justina tak do siebie pasują ze i'm in shook
#WeLoveTheEarth https://t.co/MLmyex9t1t</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row103" class="row_heading level2 row103" >2520</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row103_col0" class="data row103 col0" >90</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row103_col1" class="data row103 col1" >405</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row104" class="row_heading level0 row104" >lordefurler</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row104" class="row_heading level1 row104" >RT @lordefurler: Sia did that! #WeLoveTheEarth https://t.co/aETvluquXM</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row104" class="row_heading level2 row104" >2488</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row104_col0" class="data row104 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row104_col1" class="data row104 col1" >26</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row105" class="row_heading level0 row105" >sinsnvices</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row105" class="row_heading level1 row105" >RT @sinsnvices: utożsamiam się z brendonem  #WeLoveTheEarth https://t.co/bSLoyWD4hd</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row105" class="row_heading level2 row105" >2478</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row105_col0" class="data row105 col0" >1646</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row105_col1" class="data row105 col1" >3466</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row106" class="row_heading level0 row106" >kingoftheclout</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row106" class="row_heading level1 row106" >RT @kingoftheclout: STOP SCROLLING AND WATCH THIS VIDEO‼️ please take some time out of your day to watch this video &amp; possibly share it. it…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row106" class="row_heading level2 row106" >2124</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row106_col0" class="data row106 col0" >178</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row106_col1" class="data row106 col1" >242</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row107" class="row_heading level0 row107" >izrnsrdn</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row107" class="row_heading level1 row107" >RT @izrnsrdn: Justin Drew Bieber as a baboon 
#WeLoveTheEarth https://t.co/Wz8YK6r21q</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row107" class="row_heading level2 row107" >2034</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row107_col0" class="data row107 col0" >223</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row107_col1" class="data row107 col1" >615</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row108" class="row_heading level0 row108" >marquezduo</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row108" class="row_heading level1 row108" >RT @marquezduo: jakby ktoś się zastanawiał jak wygląda moje życie  #WeLoveTheEarth https://t.co/SLvLE6eY0V</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row108" class="row_heading level2 row108" >1906</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row108_col0" class="data row108 col0" >582</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row108_col1" class="data row108 col1" >1389</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row109" class="row_heading level0 row109" >5SecOfMendess</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row109" class="row_heading level1 row109" >RT @5SecOfMendess: Ejjj ale mi się ta piosenka serio podoba i ma genialne przesłanie!💕
#WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row109" class="row_heading level2 row109" >1870</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row109_col0" class="data row109 col0" >8</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row109_col1" class="data row109 col1" >35</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row110" class="row_heading level0 row110" >JBwakeup</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row110" class="row_heading level1 row110" >RT @JBwakeup: Ogolnie to serio glos Justina i Ariany pasuja do siebie.. chce ich colab #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row110" class="row_heading level2 row110" >1842</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row110_col0" class="data row110 col0" >14</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row110_col1" class="data row110 col1" >58</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row111" class="row_heading level0 row111" rowspan=2>MNotifiedMedia</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row111" class="row_heading level1 row111" >RT @MNotifiedMedia: Shawn Mendes the Rhino🦏 #WeLoveTheEarth https://t.co/Y2plDHsIsL</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row111" class="row_heading level2 row111" >1805</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row111_col0" class="data row111 col0" >93</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row111_col1" class="data row111 col1" >416</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row112" class="row_heading level1 row112" >RT @MNotifiedMedia: “we’re just some rhinos horny as heck” THE RHINOS ARE SO CUTE🦏  #WeLoveTheEarth https://t.co/vvkaO2U7qj</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row112" class="row_heading level2 row112" >1805</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row112_col0" class="data row112 col0" >175</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row112_col1" class="data row112 col1" >647</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row113" class="row_heading level0 row113" >DOLANVVY</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row113" class="row_heading level1 row113" >RT @DOLANVVY: Rozjebał mnie snoop dog jako marihuana, rola idealna dla niego
 #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row113" class="row_heading level2 row113" >1803</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row113_col0" class="data row113 col0" >44</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row113_col1" class="data row113 col1" >140</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row114" class="row_heading level0 row114" >justinsbicep</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row114" class="row_heading level1 row114" >RT @justinsbicep: I signed the petition. And you should too. Stream, donate and spread the message. Let's save the earth. #WeLoveTheEarth h…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row114" class="row_heading level2 row114" >1772</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row114_col0" class="data row114 col0" >58</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row114_col1" class="data row114 col1" >101</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row115" class="row_heading level0 row115" >purpxs3bizzle</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row115" class="row_heading level1 row115" >RT @purpxs3bizzle: "O homem destrói a natureza com desculpa de sobreviver, a natureza luta para sobreviver para garantir a sobrevivência do…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row115" class="row_heading level2 row115" >1716</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row115_col0" class="data row115 col0" >144</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row115_col1" class="data row115 col1" >224</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row116" class="row_heading level0 row116" >kba_yankee21</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row116" class="row_heading level1 row116" >RT @kba_yankee21: Never thought I would tear up because of a Lil Dicky song. But here I am crying in a cool way. Feel free to visit https:/…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row116" class="row_heading level2 row116" >1674</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row116_col0" class="data row116 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row116_col1" class="data row116 col1" >6</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row117" class="row_heading level0 row117" >beth_powell1</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row117" class="row_heading level1 row117" >RT @beth_powell1: LETS SAVE THE PLANET #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row117" class="row_heading level2 row117" >1629</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row117_col0" class="data row117 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row117_col1" class="data row117 col1" >0</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row118" class="row_heading level0 row118" >piggzyneedy</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row118" class="row_heading level1 row118" >RT @piggzyneedy: i see so many people tweeting about saving the planet but i bet my whole life the majority of those people are only tweeti…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row118" class="row_heading level2 row118" >1577</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row118_col0" class="data row118 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row118_col1" class="data row118 col1" >2</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row119" class="row_heading level0 row119" >particularangel</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row119" class="row_heading level1 row119" >RT @particularangel: i mean we should all listen to this part specifically #WeLoveTheEarth https://t.co/tgGZKRgXV2</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row119" class="row_heading level2 row119" >1511</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row119_col0" class="data row119 col0" >1147</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row119_col1" class="data row119 col1" >2259</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row120" class="row_heading level0 row120" >avisbelieberboy</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row120" class="row_heading level1 row120" >RT @avisbelieberboy: De lo mejor que va del año  #WeLoveTheEarth https://t.co/vN7wPOGork</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row120" class="row_heading level2 row120" >1367</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row120_col0" class="data row120 col0" >3</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row120_col1" class="data row120 col1" >4</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row121" class="row_heading level0 row121" >biebrforro</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row121" class="row_heading level1 row121" >RT @biebrforro: justin y ariana cantando juntos es lo mejor que puede existir  #WeLoveTheEarth https://t.co/Dilro999ds</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row121" class="row_heading level2 row121" >1352</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row121_col0" class="data row121 col0" >292</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row121_col1" class="data row121 col1" >626</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row122" class="row_heading level0 row122" >shawnnsbabyy</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row122" class="row_heading level1 row122" >RT @shawnnsbabyy: Il rinoceronte con la voce più bella del mondo🥰

#WeLoveTheEarth https://t.co/aSQgvumgKl</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row122" class="row_heading level2 row122" >1314</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row122_col0" class="data row122 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row122_col1" class="data row122 col1" >6</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row123" class="row_heading level0 row123" >br_atd</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row123" class="row_heading level1 row123" >RT @br_atd: O melhor porco gordo do universo !!!

 #WeLoveTheEarth https://t.co/lJfZkgnkWI</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row123" class="row_heading level2 row123" >1249</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row123_col0" class="data row123 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row123_col1" class="data row123 col1" >1</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row124" class="row_heading level0 row124" >moarjustln</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row124" class="row_heading level1 row124" >RT @moarjustln: can't believe we listened to justin's voice after months and I still in love 
#WeLoveTheEarth https://t.co/JhFRENhOH3</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row124" class="row_heading level2 row124" >1216</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row124_col0" class="data row124 col0" >58</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row124_col1" class="data row124 col1" >158</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row125" class="row_heading level0 row125" >AGPLOfficial</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row125" class="row_heading level1 row125" >RT @AGPLOfficial: Nawet gdy jest zebrą, Ariana zawsze serwuje wokal! 🎶 #WeLoveTheEarth 

Posłuchaj utworu “Earth” z Arianą Grande i plejadą…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row125" class="row_heading level2 row125" >1152</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row125_col0" class="data row125 col0" >52</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row125_col1" class="data row125 col1" >166</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row126" class="row_heading level0 row126" >xmendesly</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row126" class="row_heading level1 row126" >RT @xmendesly: stream earth by lil dicky
#WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row126" class="row_heading level2 row126" >1129</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row126_col0" class="data row126 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row126_col1" class="data row126 col1" >0</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row127" class="row_heading level0 row127" >sourdieselzain</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row127" class="row_heading level1 row127" >RT @sourdieselzain: “I’m a fat fucking pig” no ja się tu poplacze zaraz  
#WeLoveTheEarth #EarthMusicVideo https://t.co/tpBQZeRQEh</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row127" class="row_heading level2 row127" >1048</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row127_col0" class="data row127 col0" >34</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row127_col1" class="data row127 col1" >99</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row128" class="row_heading level0 row128" >MrtummyV</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row128" class="row_heading level1 row128" >RT @MrtummyV: This is so cute!! aslskfjdkskskkskak
#WeLoveTheEarth

 https://t.co/ZKKKNFQ1Wf</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row128" class="row_heading level2 row128" >1005</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row128_col0" class="data row128 col0" >10</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row128_col1" class="data row128 col1" >45</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row129" class="row_heading level0 row129" >ringsofmendes</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row129" class="row_heading level1 row129" >RT @ringsofmendes: głos ari tutaj &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;
#WeLoveTheEarth https://t.co/QDBVWZ0aom</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row129" class="row_heading level2 row129" >1005</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row129_col0" class="data row129 col0" >22</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row129_col1" class="data row129 col1" >119</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row130" class="row_heading level0 row130" >chimmybby</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row130" class="row_heading level1 row130" >RT @chimmybby: We Also Love The Sun 🌞
#WeLoveTheEarth https://t.co/mh9gfO6Z30</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row130" class="row_heading level2 row130" >1004</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row130_col0" class="data row130 col0" >34</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row130_col1" class="data row130 col1" >129</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row131" class="row_heading level0 row131" >PManice</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row131" class="row_heading level1 row131" >RT @PManice: “I’m a koala and I sleep all the time. So what? It’s cute.” 😍 #WeLoveTheEarth https://t.co/vyOvLY4bSE</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row131" class="row_heading level2 row131" >979</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row131_col0" class="data row131 col0" >33</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row131_col1" class="data row131 col1" >107</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row132" class="row_heading level0 row132" >awanasghena</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row132" class="row_heading level1 row132" >RT @awanasghena: KATY IN TENDENZA IN ITALIA. PIANGO😭🔥❤️
#ConCalmaRemix #WeLoveTheEarth https://t.co/CGnsmSd1gM</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row132" class="row_heading level2 row132" >895</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row132_col0" class="data row132 col0" >7</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row132_col1" class="data row132 col1" >14</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row133" class="row_heading level0 row133" rowspan=2>opssmymendes</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row133" class="row_heading level1 row133" >RT @opssmymendes: bardzo mi się podoba to, że można kupić merch i pieniądze z tego idą na ratowanie naszej planety #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row133" class="row_heading level2 row133" >849</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row133_col0" class="data row133 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row133_col1" class="data row133 col1" >2</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row134" class="row_heading level1 row134" >RT @opssmymendes: warto sobie wejść na stronę https://t.co/JyL7e4jrbv i poczytać o co chodzi z każdym zwierzęciem #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row134" class="row_heading level2 row134" >849</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row134_col0" class="data row134 col0" >84</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row134_col1" class="data row134 col1" >112</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row135" class="row_heading level0 row135" >_Sunfflower_</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row135" class="row_heading level1 row135" >RT @_Sunfflower_: TA PIOSENKA TO ZŁOTO I DIAMENTY
Oby jej przekaz nie skończył się tylko tylko na tym, że ludzie będą ją kojarzyli, bo spok…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row135" class="row_heading level2 row135" >784</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row135_col0" class="data row135 col0" >164</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row135_col1" class="data row135 col1" >480</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row136" class="row_heading level0 row136" >jaguareffects</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row136" class="row_heading level1 row136" >RT @jaguareffects: eu prestando atenção no áudio pra identificar cada artista

#WeLoveTheEarth https://t.co/0cDtiV2t1E</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row136" class="row_heading level2 row136" >771</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row136_col0" class="data row136 col0" >253</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row136_col1" class="data row136 col1" >380</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row137" class="row_heading level0 row137" >cerberusgrande</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row137" class="row_heading level1 row137" >RT @cerberusgrande: wszyscy mówią jak bardzo chcieliby usłyszeć biebera i ariane (same), ale ja bym chciała usłyszeć ariana x halsey, którą…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row137" class="row_heading level2 row137" >759</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row137_col0" class="data row137 col0" >3</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row137_col1" class="data row137 col1" >7</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row138" class="row_heading level0 row138" >suplisamanobal</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row138" class="row_heading level1 row138" >RT @suplisamanobal: Not blackpink related but Lil dicky x justin bieber, ft ariana grande, and shawn mendes, also charlie puth, and sia and…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row138" class="row_heading level2 row138" >740</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row138_col0" class="data row138 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row138_col1" class="data row138 col1" >6</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row139" class="row_heading level0 row139" rowspan=3>Yuuupthatsme</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row139" class="row_heading level1 row139" >RT @Yuuupthatsme: Jestem pod wrażeniem, że lil dicky był w stanie pokazać tak poważny problem w taki przyjemny sposób
#WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row139" class="row_heading level2 row139" >669</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row139_col0" class="data row139 col0" >464</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row139_col1" class="data row139 col1" >1256</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row140" class="row_heading level1 row140" >RT @Yuuupthatsme: TEGO SIĘ NIE SPODZIEWAŁAM XD
#WeLoveTheEarth https://t.co/VuhRNdhcV7</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row140" class="row_heading level2 row140" >669</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row140_col0" class="data row140 col0" >70</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row140_col1" class="data row140 col1" >316</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row141" class="row_heading level1 row141" >RT @Yuuupthatsme: Miałeś być żyrafą #WeLoveTheEarth https://t.co/0kNCpU8o6q</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row141" class="row_heading level2 row141" >669</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row141_col0" class="data row141 col0" >8</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row141_col1" class="data row141 col1" >56</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row142" class="row_heading level0 row142" >thremptyworlds</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row142" class="row_heading level1 row142" >RT @thremptyworlds: piosenka jest cudowna, tylko brakuje mi takiego momentu w ktorym wszyscy razem zaspiewaliby refren... #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row142" class="row_heading level2 row142" >629</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row142_col0" class="data row142 col0" >55</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row142_col1" class="data row142 col1" >215</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row143" class="row_heading level0 row143" >typicalbizzzle</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row143" class="row_heading level1 row143" >RT @typicalbizzzle: This song and music video had such a powerful and great message it. It’s a wake up call for the whole woltd to get the…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row143" class="row_heading level2 row143" >601</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row143_col0" class="data row143 col0" >694</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row143_col1" class="data row143 col1" >1116</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row144" class="row_heading level0 row144" >liveforshawn02</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row144" class="row_heading level1 row144" >RT @liveforshawn02: This is one of the most beautiful concepts for a video ever! I’m so proud and thankful of @shawnmendes❤️ @lildickytweet…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row144" class="row_heading level2 row144" >578</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row144_col0" class="data row144 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row144_col1" class="data row144 col1" >3</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row145" class="row_heading level0 row145" >aurelialmao</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row145" class="row_heading level1 row145" >RT @aurelialmao: Uważam, że tą piosenkę powinni znać wszyscy, bo może wtedy kogoś ruszy stan naszej planety #EarthMusicVideo #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row145" class="row_heading level2 row145" >572</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row145_col0" class="data row145 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row145_col1" class="data row145 col1" >2</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row146" class="row_heading level0 row146" >jaileystation</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row146" class="row_heading level1 row146" >RT @jaileystation: PERO USTEDES ESCUCHARON A ED SHEERAN SIENDO EL KOALA MAS TIERNO QUE EXISTE #WeLoveTheEarth https://t.co/UvmXmy5E1C</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row146" class="row_heading level2 row146" >546</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row146_col0" class="data row146 col0" >332</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row146_col1" class="data row146 col1" >852</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row147" class="row_heading level0 row147" >athenajasvier</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row147" class="row_heading level1 row147" >RT @athenajasvier: lil dicky is amazing #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row147" class="row_heading level2 row147" >546</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row147_col0" class="data row147 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row147_col1" class="data row147 col1" >0</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row148" class="row_heading level0 row148" >llostinmyouth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row148" class="row_heading level1 row148" >RT @llostinmyouth: Ed versione koala è il mio stile di vita dal lunedì alla domenica #WeLoveTheEarth https://t.co/MbhaMaVaRD</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row148" class="row_heading level2 row148" >520</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row148_col0" class="data row148 col0" >11</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row148_col1" class="data row148 col1" >34</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row149" class="row_heading level0 row149" >MercurySimons</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row149" class="row_heading level1 row149" >RT @MercurySimons: everybody should be listening to this masterpiece, the planet really needs our help and it shouldn't take a song with a…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row149" class="row_heading level2 row149" >516</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row149_col0" class="data row149 col0" >275</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row149_col1" class="data row149 col1" >489</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row150" class="row_heading level0 row150" >realestbeach</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row150" class="row_heading level1 row150" >RT @realestbeach: if y’all love the earth, start acting like it. pollution is real and y’all need to start taking it seriously!!  #WeLoveTh…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row150" class="row_heading level2 row150" >504</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row150_col0" class="data row150 col0" >354</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row150_col1" class="data row150 col1" >681</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row151" class="row_heading level0 row151" rowspan=9>Piatt_Futuro</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row151" class="row_heading level1 row151" >RT @Piatt_Futuro: Edilizia motore di rigenerazione urbana. #4future #19aprile #fridaysforfuture ☀️ #WeLoveTheEarth
https://t.co/TdVCrj86L8</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row151" class="row_heading level2 row151" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row151_col0" class="data row151 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row151_col1" class="data row151 col1" >5</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row152" class="row_heading level1 row152" >RT @Piatt_Futuro: Il nostro "ius soli":  terra, suolo e prodotti agricoli 🇮🇹 nel mondo. #4future #19aprile #fridaysforfuture ☀️ #WeLoveTheE…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row152" class="row_heading level2 row152" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row152_col0" class="data row152 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row152_col1" class="data row152 col1" >4</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row153" class="row_heading level1 row153" >RT @Piatt_Futuro: L'ambiente è la leva dello sviluppo economico. #4future #19aprile #fridaysforfuture
#WeLoveTheEarth
https://t.co/TdVCrj86…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row153" class="row_heading level2 row153" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row153_col0" class="data row153 col0" >5</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row153_col1" class="data row153 col1" >5</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row154" class="row_heading level1 row154" >RT @Piatt_Futuro: La persona al centro, l'ambiente intorno. #4future #19aprile ☀️ #fridaysforfuture #WeLoveTheEarth
https://t.co/TdVCrj86L8</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row154" class="row_heading level2 row154" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row154_col0" class="data row154 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row154_col1" class="data row154 col1" >6</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row155" class="row_heading level1 row155" >RT @Piatt_Futuro: Meno gomma, più ferro: trasporti veloci sicuri e non inquinanti. #4future #19aprile #fridaysforfuture ☀️ #WeLoveTheEarth…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row155" class="row_heading level2 row155" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row155_col0" class="data row155 col0" >5</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row155_col1" class="data row155 col1" >6</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row156" class="row_heading level1 row156" >RT @Piatt_Futuro: Riscaldamento globale: soluzioni, non fake news! #4future #19aprile #fridaysforfuture ☀️ #WeLoveTheEarth
https://t.co/TdV…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row156" class="row_heading level2 row156" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row156_col0" class="data row156 col0" >12</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row156_col1" class="data row156 col1" >12</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row157" class="row_heading level1 row157" >RT @Piatt_Futuro: Più mercato e concorrenza per l'accesso di tutti  all'acqua, meno sprechi e inefficienze. #4future #19aprile #fridaysforf…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row157" class="row_heading level2 row157" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row157_col0" class="data row157 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row157_col1" class="data row157 col1" >1</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row158" class="row_heading level1 row158" >RT @Piatt_Futuro: Un grande sconto fiscale per l'ambiente! #4future #19aprile #fridaysforfuture ☀️ #WeLoveTheEarth
https://t.co/TdVCrj86L8</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row158" class="row_heading level2 row158" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row158_col0" class="data row158 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row158_col1" class="data row158 col1" >6</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row159" class="row_heading level1 row159" >RT @Piatt_Futuro: Riciclo riuso e termocombustori: Italia pulita, meno malavita. #4future #19aprile #fridaysforfuture ☀️
#WeLoveTheEarth
ht…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row159" class="row_heading level2 row159" >427</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row159_col0" class="data row159 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row159_col1" class="data row159 col1" >8</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row160" class="row_heading level0 row160" >vanessaibanez_</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row160" class="row_heading level1 row160" >RT @vanessaibanez_: artists using their platform to spread awareness, kudos!! stream the song #WeLoveTheEarth https://t.co/nID21ksupN</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row160" class="row_heading level2 row160" >416</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row160_col0" class="data row160 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row160_col1" class="data row160 col1" >1</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row161" class="row_heading level0 row161" >Adryelli_Godoi</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row161" class="row_heading level1 row161" >RT @Adryelli_Godoi: Justin/ Babuíno: Nós vamos morrer?!
Lil Dicky: Sabe, Bieber nós podemos morrer. Eu não vou mentir pra você. Há muitas p…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row161" class="row_heading level2 row161" >387</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row161_col0" class="data row161 col0" >629</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row161_col1" class="data row161 col1" >1095</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row162" class="row_heading level0 row162" >fayessflatline</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row162" class="row_heading level1 row162" >RT @fayessflatline: This is some true shit #WeLoveTheEarth https://t.co/MLYY7v3JAL</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row162" class="row_heading level2 row162" >381</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row162_col0" class="data row162 col0" >8220</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row162_col1" class="data row162 col1" >16514</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row163" class="row_heading level0 row163" >brian_prism</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row163" class="row_heading level1 row163" >RT @brian_prism: #ConCalmaRemix &amp; #WeLoveTheEarth  Tonight🔥 https://t.co/EjQbaYZYmu</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row163" class="row_heading level2 row163" >348</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row163_col0" class="data row163 col0" >16</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row163_col1" class="data row163 col1" >22</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row164" class="row_heading level0 row164" >Clausbelieberj</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row164" class="row_heading level1 row164" >RT @Clausbelieberj: progetto meraviglioso, vederlo mi ha emozionata.
coinvolgere così tanti artisti per un buona causa è una cosa bellissim…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row164" class="row_heading level2 row164" >337</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row164_col0" class="data row164 col0" >14</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row164_col1" class="data row164 col1" >68</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row165" class="row_heading level0 row165" rowspan=2>ver0017</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row165" class="row_heading level1 row165" >RT @ver0017: oni doskonale wiedzą, że handwritten przyczyniło się do uratowania naszej planety #WeLoveTheEarth https://t.co/XF0JvxrerA</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row165" class="row_heading level2 row165" >288</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row165_col0" class="data row165 col0" >9</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row165_col1" class="data row165 col1" >42</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row166" class="row_heading level1 row166" >RT @ver0017: ciekawi mnie na jakiej podstawie dobierali zwierzęta do artystów 😂🤔 #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row166" class="row_heading level2 row166" >288</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row166_col0" class="data row166 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row166_col1" class="data row166 col1" >2</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row167" class="row_heading level0 row167" >dsakrv</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row167" class="row_heading level1 row167" >RT @dsakrv: Lil Dicky - Earth (Official Music Video) https://t.co/M5TtrumWYQ via @YouTube #WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row167" class="row_heading level2 row167" >239</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row167_col0" class="data row167 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row167_col1" class="data row167 col1" >1</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row168" class="row_heading level0 row168" >CelebrityArticl</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row168" class="row_heading level1 row168" >RT @CelebrityArticl: #ArianaGrande Opens Up About the Darkish Facet of Performing Her New #music “It Is Hell” #Singer #CelebrityNews #WeLov…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row168" class="row_heading level2 row168" >217</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row168_col0" class="data row168 col0" >3</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row168_col1" class="data row168 col1" >2</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row169" class="row_heading level0 row169" >Ws_Vinicius</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row169" class="row_heading level1 row169" >RT @Ws_Vinicius: O Brasil não foi esquecido no churrasco, Rio representando manooo, com os vocais da Ariana de fundo. QUE HINOOOOOOOO EU AM…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row169" class="row_heading level2 row169" >215</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row169_col0" class="data row169 col0" >224</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row169_col1" class="data row169 col1" >516</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row170" class="row_heading level0 row170" >sevenyearsbiebs</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row170" class="row_heading level1 row170" >RT @sevenyearsbiebs: oby wiadomość zawarta w piosence trafiła do dużej ilości osób, może dzięki temu świat zacznie się zmieniać na lepsze…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row170" class="row_heading level2 row170" >214</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row170_col0" class="data row170 col0" >546</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row170_col1" class="data row170 col1" >1083</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row171" class="row_heading level0 row171" >ShawnDailyJP</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row171" class="row_heading level1 row171" >RT @ShawnDailyJP: Lil Dickyの新曲・チャリティーソング「Earth」
アリアナ・ジャスティン・カニエら名だたるアーティスト達と共にショーンも参加してます。
是非聴いてみて下さい。
#WeLoveTheEarth 
https://t.co/CKUtq0…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row171" class="row_heading level2 row171" >199</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row171_col0" class="data row171 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row171_col1" class="data row171 col1" >6</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row172" class="row_heading level0 row172" >Joprojekt</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row172" class="row_heading level1 row172" >RT @Joprojekt: #WeLoveTheEarth Dire que #LinkinPark a écrit deux albums magnifiques sur l'environnement (pas seulement) #AThousandSuns et #…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row172" class="row_heading level2 row172" >182</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row172_col0" class="data row172 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row172_col1" class="data row172 col1" >3</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row173" class="row_heading level0 row173" >justinsmiIxs</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row173" class="row_heading level1 row173" >RT @justinsmiIxs: "Ya sé que no todos somos iguales, pero vivimos en la misma tierra"  
"¿Vamos a morir?" 
"Sabes Bieber? No te voy a menti…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row173" class="row_heading level2 row173" >171</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row173_col0" class="data row173 col0" >530</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row173_col1" class="data row173 col1" >762</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row174" class="row_heading level0 row174" >jujustinbieeber</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row174" class="row_heading level1 row174" >RT @jujustinbieeber: Que la canción y el video no se quede solo un momento y creamos conciencia del daño que hacemos a los animales, al pla…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row174" class="row_heading level2 row174" >167</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row174_col0" class="data row174 col0" >115</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row174_col1" class="data row174 col1" >178</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row175" class="row_heading level0 row175" >sgxjbstylesoft</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row175" class="row_heading level1 row175" >RT @sgxjbstylesoft: la voz de todos esos artistas tan talentosos ha quedado perfecta, amo que se hayan juntando para dejar ese mensaje tan…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row175" class="row_heading level2 row175" >156</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row175_col0" class="data row175 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row175_col1" class="data row175 col1" >1</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row176" class="row_heading level0 row176" rowspan=2>jestemzajeta</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row176" class="row_heading level1 row176" >RT @jestemzajeta: uzbierane pieniądze trafiają na fundację Leonardo DiCaprio, która ratuje naszą planetę 
#WeLoveTheEarth</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row176" class="row_heading level2 row176" >143</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row176_col0" class="data row176 col0" >504</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row176_col1" class="data row176 col1" >1218</td>
            </tr>
            <tr>
                                <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row177" class="row_heading level1 row177" >RT @jestemzajeta: Shawn jest nosorożecem
Halsey lwiątkiem
Charlie Puth żyrafą
Ed Sheeran koalą
Sia kangurem 
miley słoniem 
Ariana zebrą 
K…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row177" class="row_heading level2 row177" >143</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row177_col0" class="data row177 col0" >126</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row177_col1" class="data row177 col1" >408</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row178" class="row_heading level0 row178" >itszGabbs</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row178" class="row_heading level1 row178" >RT @itszGabbs: OUÇAM EARTH! O clipe é o incrível, a música mais ainda e todo dinheiro arrecadado com a música será doado para a instituição…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row178" class="row_heading level2 row178" >105</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row178_col0" class="data row178 col0" >72</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row178_col1" class="data row178 col1" >105</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row179" class="row_heading level0 row179" >Clem_rocher</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row179" class="row_heading level1 row179" >RT @Clem_rocher: Justin Bieber, Ariana Grande, Wiz Khalifa, Shawn Mendes, Ed Sheeran, Rita Ora... de nombreux artistes se mobilisent autour…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row179" class="row_heading level2 row179" >99</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row179_col0" class="data row179 col0" >30</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row179_col1" class="data row179 col1" >54</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row180" class="row_heading level0 row180" >OursPooh</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row180" class="row_heading level1 row180" >RT @OursPooh: we love the earth, it is our planet
we love the earth, it is our home #WeLoveTheEarth https://t.co/NXUhU758uQ</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row180" class="row_heading level2 row180" >98</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row180_col0" class="data row180 col0" >85</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row180_col1" class="data row180 col1" >263</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row181" class="row_heading level0 row181" >soulsfiend</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row181" class="row_heading level1 row181" >RT @soulsfiend: mais les gens qui sont là à se plaindre « gngngn j’aime pas la chanson » vous pouvez connecter vos 2 neurones 2 secondes ?…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row181" class="row_heading level2 row181" >82</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row181_col0" class="data row181 col0" >24</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row181_col1" class="data row181 col1" >35</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row182" class="row_heading level0 row182" >introandrew</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row182" class="row_heading level1 row182" >RT @introandrew: #WeLoveTheEarth é un progetto molto importante,oltre ad essere una canzone,vuole lanciare un messaggio,il SALVARE LA TERRA…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row182" class="row_heading level2 row182" >81</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row182_col0" class="data row182 col0" >53</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row182_col1" class="data row182 col1" >119</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row183" class="row_heading level0 row183" >twentysevenmoon</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row183" class="row_heading level1 row183" >RT @twentysevenmoon: i recommend you guys go watch Our Planet on netflix. it made me cry and i hope it motivates you to take action on savi…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row183" class="row_heading level2 row183" >75</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row183_col0" class="data row183 col0" >106</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row183_col1" class="data row183 col1" >274</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row184" class="row_heading level0 row184" >camillazambett2</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row184" class="row_heading level1 row184" >RT @camillazambett2: Spero che con questa collaborazione arrivi a tutti il messaggio di salvare la Terra!🌍❤️
 #WeLoveTheEarth https://t.co/…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row184" class="row_heading level2 row184" >74</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row184_col0" class="data row184 col0" >3</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row184_col1" class="data row184 col1" >0</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row185" class="row_heading level0 row185" >bemybizzle_</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row185" class="row_heading level1 row185" >RT @bemybizzle_: Justin and Ariana they both sounds so damn good it's just wow !!!!
#WeLoveTheEarth https://t.co/9aRwrD6i9J</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row185" class="row_heading level2 row185" >67</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row185_col0" class="data row185 col0" >762</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row185_col1" class="data row185 col1" >1911</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row186" class="row_heading level0 row186" >xjbtalentedx</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row186" class="row_heading level1 row186" >RT @xjbtalentedx: Yo podría ver y ver éste vídeo nunca me aburriría... ♡

#WeLoveTheEarth https://t.co/HdLb55CNcA</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row186" class="row_heading level2 row186" >58</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row186_col0" class="data row186 col0" >63</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row186_col1" class="data row186 col1" >171</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row187" class="row_heading level0 row187" >__alfredo30__</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row187" class="row_heading level1 row187" >RT @__alfredo30__: Questa canzone è bellissima.
Speriamo riesca a sensibilizzare più persone possibili su questo enorme pericolo 🌍
#WeLoveT…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row187" class="row_heading level2 row187" >55</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row187_col0" class="data row187 col0" >4</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row187_col1" class="data row187 col1" >7</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row188" class="row_heading level0 row188" >protectmayne</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row188" class="row_heading level1 row188" >RT @protectmayne: Earth se tornou minha música preferida junto com o clipe 
isso simplesmente por passar uma mensagem forte pra gente, eu e…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row188" class="row_heading level2 row188" >40</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row188_col0" class="data row188 col0" >294</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row188_col1" class="data row188 col1" >562</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row189" class="row_heading level0 row189" >fabiannn___29</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row189" class="row_heading level1 row189" >RT @fabiannn___29: Me encantaría tanto que esta canción fuera #1 no solo en USA o UK si no en muchos países del mundo. Ojalá que le den el…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row189" class="row_heading level2 row189" >37</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row189_col0" class="data row189 col0" >5</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row189_col1" class="data row189 col1" >8</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row190" class="row_heading level0 row190" >4miraizat</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row190" class="row_heading level1 row190" >RT @4miraizat: ed sheeran(and koala) is my spirit animal #WeLoveTheEarth https://t.co/VYTPuAajM6</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row190" class="row_heading level2 row190" >28</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row190_col0" class="data row190 col0" >68</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row190_col1" class="data row190 col1" >181</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row191" class="row_heading level0 row191" >LILG96958980</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row191" class="row_heading level1 row191" >RT @LILG96958980: Me on my way to save the earth after bobbing to the song  for a straight hour 
#WeLoveTheEarth https://t.co/94g0N2SLBM</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row191" class="row_heading level2 row191" >24</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row191_col0" class="data row191 col0" >1224</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row191_col1" class="data row191 col1" >3448</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row192" class="row_heading level0 row192" >KeyNarumi</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row192" class="row_heading level1 row192" >RT @KeyNarumi: Ini keren sumpah. Pesannya tuh bener bikin lo mikir apa aja yg udah lo lakuin untuk Bumi Kita dengan visual yang menyenangka…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row192" class="row_heading level2 row192" >18</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row192_col0" class="data row192 col0" >1</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row192_col1" class="data row192 col1" >0</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row193" class="row_heading level0 row193" >Yuberli_Rosario</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row193" class="row_heading level1 row193" >RT @Yuberli_Rosario: “Todos estos tiroteos, la contaminación. Nos atacamos a nosotros mismos. Vamos a relajarnos, respeta lo que construimo…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row193" class="row_heading level2 row193" >17</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row193_col0" class="data row193 col0" >24</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row193_col1" class="data row193 col1" >54</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row194" class="row_heading level0 row194" >bieber_najaFC</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row194" class="row_heading level1 row194" >RT @bieber_najaFC: Com o coração quentinho depois de ver que realmente tem pessoas que se importam com o nosso planeta. #WeLoveTheEarth htt…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row194" class="row_heading level2 row194" >14</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row194_col0" class="data row194 col0" >26</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row194_col1" class="data row194 col1" >69</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row195" class="row_heading level0 row195" >khaliqhaiqal_</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row195" class="row_heading level1 row195" >RT @khaliqhaiqal_: Marvel : "Avengers Endgame is gonna be the most ambitious crossover event in history"

Lil Dicky : *hold my beer*
@lildi…</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row195" class="row_heading level2 row195" >13</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row195_col0" class="data row195 col0" >2151</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row195_col1" class="data row195 col1" >5487</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row196" class="row_heading level0 row196" >martyydg</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row196" class="row_heading level1 row196" >RT @martyydg: Semplicemente MERAVIGLIOSO #WeLoveTheEarth https://t.co/m6I2J2soEe</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row196" class="row_heading level2 row196" >12</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row196_col0" class="data row196 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row196_col1" class="data row196 col1" >2</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row197" class="row_heading level0 row197" >biebermylife946</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row197" class="row_heading level1 row197" >RT @biebermylife946: Salviamo il posto in cui viviamo,acquistando la canzone daremo una speranza. #WeLoveTheEarth https://t.co/6OmM8oAvhG</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row197" class="row_heading level2 row197" >12</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row197_col0" class="data row197 col0" >2</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row197_col1" class="data row197 col1" >2</td>
            </tr>
            <tr>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level0_row198" class="row_heading level0 row198" >Malikjvvd</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level1_row198" class="row_heading level1 row198" >RT @Malikjvvd: Uwuuu uwuuuuuu
#WeLoveTheEarth https://t.co/WtVzUrVJW1</th>
                        <th id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0level2_row198" class="row_heading level2 row198" >1</th>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row198_col0" class="data row198 col0" >64</td>
                        <td id="T_fbe77a0e_fee6_11ed_af86_9ef7402596b0row198_col1" class="data row198 col1" >208</td>
            </tr>
    </tbody></table>

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors
    
def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])


def test_df_creation_command():
    assert 'retweets' in last_input, \
        "The input data for DataFrame creation is not as expected."
    assert 'columns=' in last_input, \
        "The columns parameter is missing."
    assert 'groupby' in last_input, \
        "The groupby method is missing."
    assert 'sum()' in last_input, \
        "The sum method is missing."
    assert 'sort_values' in last_input, \
        "The sort_values method is missing."
    assert 'ascending' in last_input, \
        "The ascending parameter is missing."
    
def test_dataframe():
    correct_dataframe = pd.DataFrame(retweets, columns=['Retweets','Favorites', 'Followers', 'ScreenName', 'Text']).groupby(
    ['ScreenName','Text','Followers']).sum().sort_values(by=['Followers'], ascending=False)
    assert correct_dataframe.equals(df), \
    "The created dataframe does not match the expected dataframe."
```

    2/2 tests passed

## 9. Analyzing used languages
<p>🕵️‍♀️ Our table tells us that:</p>
<ul>
<li>Lil Dicky's followers reacted the most — 42.4% of his followers liked his first tweet. </li>
<li>Even if celebrities like Katy Perry and Ellen have a huuge Twitter following, their followers hardly reacted, e.g., only 0.0098% of Katy's followers liked her tweet. </li>
<li>While Leo got the most likes and retweets in terms of counts, his first tweet was only liked by 2.19% of his followers. </li>
</ul>
<p>The large differences in reactions could be explained by the fact that this was Lil Dicky's music video. Leo still got more traction than Katy or Ellen because he played some major role in this initiative.</p>
<hr>
<p>Can we find some more interesting patterns in the data? From the text of the tweets, we could spot different languages, so let's create a frequency distribution for the languages.</p>

```python
# Extracting language for each tweet and appending it to the list of languages
tweets_languages = []
for tweet in tweets:
        tweets_languages.append(tweet['lang'])

# Plotting the distribution of languages
%matplotlib inline
plt.hist(tweets_languages)
```

    (array([303., 107.,  22.,  14.,  36.,  32.,   3.,   2.,   1.,   2.]),
     array([ 0. ,  1.3,  2.6,  3.9,  5.2,  6.5,  7.8,  9.1, 10.4, 11.7, 13. ]),
     <a list of 10 Patch objects>)

![png](images/output_25_1.png)

```python
# One or more tests of the student's code
# The @solution should pass the tests
# The purpose of the tests is to try to catch common errors and
# to give the student a hint on how to resolve these errors

def test_tweet_languages():
    correct_tweet_languages = []
    for tweet in tweets: correct_tweet_languages.append(tweet['lang'])
    assert correct_tweet_languages == tweets_languages, \
    "The tweets_languages variable does not have the expected values."
    
last_value = _

def test_plot_exists():
    assert type(last_value) == type(plt.hist(tweets_languages)), \
    'A plot was not the last output of the code cell.'

def strip_comment_lines(cell_input):
    """Returns cell input string with comment lines removed."""
    return '\n'.join(line for line in cell_input.splitlines() if not line.startswith('#'))

last_input = strip_comment_lines(In[-2])

def test_plot_command():
    assert 'plt.hist(tweets_languages)' in last_input, \
        "We expected the plt.hist() method in your input."   
```

    3/3 tests passed

![png](images/output_26_2.png)

## 10. Final thoughts
<p>🕵️‍♀️ The last histogram tells us that:</p>
<ul>
<li>Most of the tweets were in English.</li>
<li>Polish, Italian and Spanish were the next runner-ups. </li>
<li>There were a lot of tweets with a language alien to Twitter (lang = 'und'). </li>
</ul>
<p>Why is this sort of information useful? Because it can allow us to get an understanding of the "category" of people interested in this topic (clustering). We could also analyze the device type used by the Twitteratis, <code>tweet['source']</code>, to answer questions like, <strong>"Does owning an Apple compared to Andorid influences people's propensity towards this trend?"</strong>. I will leave that as a <strong>further exercise</strong> for you!</p>
<p><img src="https://assets.datacamp.com/production/project_760/img/languages_world_map.png" style="width: 500px"></p>
<hr>
<p><span style="color:#41859e">
What an exciting journey it has been! We started almost clueless, and here we are.. rich in insights. </span></p>
<p><span style="color:#41859e">
From location based comparisons to analyzing the activity around a tweet to finding patterns from languages and devices, we have covered a lot today — let's give ourselves <b>a well-deserved pat on the back!</b> ✋
</span>
<br><br></p>
<div style="text-align: center;color:#41859e"><b><i>Magic Formula = Data + Python + Creativity + Curiosity</i></b></div>
<p><img src="https://assets.datacamp.com/production/project_760/img/finish_line.jpg" style="width: 500px"></p>

```python
# Congratulations!
print("High Five!!!")
```

    High Five!!!

```python
def test_nothing_task_10():
    assert True, "Nothing to test."
```

    1/1 tests passed

# bus
bus


from urllib.parse import urlencode, unquote
import requests
import json

url = "http://newsky2.kma.go.kr/service/SecndSrtpdFrcstInfoService2/ForecastGrib"
queryString = "?" + urlencode(
    {
        "ServiceKey" : unquote("x2SGcNH3BKOKPj8VWApv%2Fymt6NShFF%2F1LKhK48yHiDKX%2FALRldagihd%2FK2aC6WhQU32kN6GCSa%2FIE5HP2iug%2Bw%3D%3D"), 
        "base_date" : "20190407", 
        "base_time" : "1200", 
        "nx" : "59", 
        "ny" : "127", 
        "numOfRows" : "10", 
        "pageNo" : "1", 
        "_type" : "json" 
    }
)

response = requests.get(url + queryString)
print("===== response json data start =====")
print(response)
print("===== response json data end =====")
print()

r_dict = json.loads(response.text)
r_response = r_dict.get("response")
r_body = r_response.get("body")
r_items = r_body.get("items")
r_item = r_items.get("item")

result = {}
for item in r_item:
    if(item.get("category") == "T1H"):
        result = item
        break
        
print("===== response dictionary(python object) data start =====")
print(result)
print("===== response dictionary(python object) end =====")
print()

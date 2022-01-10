---
layout: post
title: Lab 2.7 - Animal Crossing Socks 
subtitle: Uddipto Nandi
---

## Objectives:
Obtain data from a web API, use Python classes to organize informatio, and use Python for data analysis. 

## Tasks:

### Task 1: Obtaining a csv from the Web API
To analyze the socks in animal crossing first we have to extract and collect the information from web API and store it somewhere. For this lab, we collected the information from the animal crossing socks API in a csv file because it allows us to easily analyze the data to perform the other tasks. 

Here is the code I used to collect the information from the API into a csv file. 
```
import requests

index = 0 
BASE_URL = "https://hm-cs.herokuapp.com"
ENDPOINT = "/socks"
API_KEY = "ArtOfDataKEY123"
payload = {'key': API_KEY, 'idx': index}
response = requests.get(BASE_URL+ENDPOINT,payload)
socks_data = response.text
print(socks_data)
index += 1

while response.ok: 
    payload = {'key': API_KEY, 'idx': index}
    response = requests.get(BASE_URL+ENDPOINT,payload)
    socks_data = response.text
    print(socks_data)
    index += 1
```
Notice how I reequested the information from the API, everytime we go to a new sock we have to use the base_url, endpoint, API key and the index of the sock. The API key and the index are reffered to as the payload, the key is required to access the site as a kind of key to a lock. The index is used to number the socks and also allow for access to a single sock, for example if I put in the index as 4, I would get the 5th sock (this is because index starts at 0). Since everytime I am requesting information from the webiste the index has to change the payload has the idx set as the variable index which we can change since it is a integer that was initially set to 0. The while loop is what does the interating, while the response from the website is okay, meaning there are no errors and there is information stored in the particular index put in the payload, it will add 1 to the index and request information from the API again. Afterwards we can convert the print sock_data into the csv file socks_data.csv. 

### Set-Up for the Rest of the Tasks

Before the rest of the tasks can be completed we have to import the csv into a python file, and make it a list so that it can be used in methods and information can be extrated/sorted even more. 

Here is the code for that: 
```
import csv
data = None 
with open("../datasets/socks.csv",encoding = "utf-8-sig") as f:
    data = list(csv.DictReader(f))
```
This code imports the csv we created adn then saves it as a list with the name data. 

#### Sock Class: 
Here is the code for my sock class: 
```
class sockType:  

    def __init__(self,name):   
        self.name = name
        self.variation = []

    def count_variations(self):
        return len(self.variation)
    
    def add_variation(self,variation):
        self.variation.append(variation)

    def __repr__(self):
        return f"{self.name},{self.variation},{self.count_variations()}"
```

The sock class was used to create sock objects. There were around 350 different socks in the API, however many of the socks were the same type of sock as others in the API, but they had different color combinations which made then seperatee objects in the API. However I wanted to use the Sock class to group all of those together. This class has a costructor method, a method to count the number of variations of a particular type of sock, and a method to add variaitons to a sock object. The repr method organizes this informations neatly for later. 

#### Variations Class
However my sock class was missing one thing. It wasn't able to store both all the variabtions of a sock and all the different colors of the sock variations. So for this reason I created a variations class. Here is the code for the variaitons class: 
```
class Variation: 
    def __init__(self,variation_name,color_1,color_2):  
        self.variation_name = variation_name
        self.color_1 = color_1
        self.color_2 = color_2
        self.marker = ":"
    
    def getColor1(self): 
        return(self.color_1)
    
    def getColor2(self): 
        return(self.color_2)

    def __repr__(self):
        return f"{self.variation_name},{self.marker},{self.color_1},{self.color_2}"
```
The variations class picked up where the Sock class left off. Like the sock method it also keeps track of variaitions, but instead of grouping them together it looks at them individually and stores their colors as well. It has a constructor method, and two get color methods to get either color 1 or 2 of a particular variation. A repr method, like before, allows me to organize this information neatly later. 

#### List All Socks

### Task 2: Which Sock Has the Most variations 

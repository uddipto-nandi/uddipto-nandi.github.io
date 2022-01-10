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

### Task 2: Which Sock Has the Most variations 

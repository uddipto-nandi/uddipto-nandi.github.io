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

#### All Socks
Now that the classes were complete I made a list to hold all of the information that classes organized. This is where the repr methods become useful, when I call an object to be placed into the dicationary, it is organized through the two repr methods of the classes. Here is the code for the all_socks dictionary: 
```
all_socks = {}

for sock in data:
    name = sock["Name"]
    variation_name = sock["Variation"]
    color_1 = sock["Color 1"]
    color_2 = sock["Color 2"]
    if color_2 == color_1: 
        color_2 = None
    variation = Variation(variation_name,color_1, color_2)
    if  name not in all_socks: 
        all_socks[name] = sockType(name)
        all_socks[name].add_variation(variation)
    else: 
        all_socks[name].add_variation(variation)
print(all_socks)
```
Here is what happens when you print all_socks: (warning its a lot!)

{'aerobics leggings': aerobics leggings,[Red & pink,:,Pink,Red, Emerald & lime,:,Green,Light blue, Purple & orange,:,Orange,Purple, Light blue & salmon pink,:,Pink,Light blue, Yellow & blue,:,Blue,Yellow],5, 'Aran-knit socks': Aran-knit socks,[Beige,:,Beige,None, White,:,White,None, Red,:,Red,None, Green,:,Green,None, Blue,:,Blue,None, Black,:,Black,None],6, 'argyle crew socks': argyle crew socks,[Blue,:,Blue,Light blue, Red,:,Red,White, Green,:,Green,Yellow, Beige,:,Beige,Brown, Gray,:,Gray,Pink, White,:,White,Red, Orange,:,Orange,White, Pink,:,Pink,White],8, 'back-bow socks': back-bow socks,[Pink,:,Pink,Black, Yellow,:,Yellow,Green, Black,:,Black,White, White,:,White,Pink, Blue,:,Light blue,Yellow, Peacock blue,:,Green,Pink],6, 'bobby socks': bobby socks,[White,:,White,None, Gray,:,Gray,None, Black,:,Black,None, Brown,:,Brown,None],4, 'color-blocked socks': color-blocked socks,[Purple,:,Purple,Colorful, Green,:,Green,Colorful, Brown,:,Brown,Colorful, Blue,:,Blue,Colorful, Beige,:,Beige,Colorful, White,:,White,Colorful, Lime,:,Green,Colorful, Pink,:,Pink,Colorful],8, 'compression tights': compression tights,[Blue,:,Black,Blue, Yellow,:,Black,Yellow, Pink,:,Black,Pink, Mint,:,Black,Green, Red,:,Black,Red],5, 'country socks': country socks,[Red ribbons,:,White,Red, Green ribbons,:,White,Green, Blue ribbons,:,White,Blue, Black ribbons,:,White,Black],4, 'crocheted socks': crocheted socks,[Beige,:,Beige,None, Gray,:,Gray,None, Purple,:,Pink,None, Blue,:,Light blue,None],4, 'denim leggings': denim leggings,[Blue,:,Blue,None, Indigo blue,:,Blue,None, Saxon blue,:,Light blue,None, Light blue,:,Light blue,None],4, 'dotted knee-high socks': dotted knee-high socks,[Black,:,Black,None, Yellow,:,Yellow,None, Cyan,:,Green,None, Gray,:,Gray,None],4, 'embroidered-flower tights': embroidered-flower tights,[Brown,:,Brown,Red, Black,:,Black,White, Green,:,Green,Yellow, Beige,:,Beige,Red, Blue,:,Blue,Orange, Purple,:,Purple,Pink],6, 'everyday socks': everyday socks,[Brown,:,Brown,None, Black,:,Black,None, Navy blue,:,Blue,None, Gray,:,Gray,None, Beige,:,Beige,None, White,:,White,None],6, 'everyday tights': everyday tights,[Black,:,Black,None, Light gray,:,Gray,None, Gray,:,Gray,None, White,:,White,None, Navy blue,:,Blue,None, Beige,:,Beige,None],6, 'fishnet tights': fishnet tights,[Black,:,Black,None, White,:,White,None, Red,:,Red,None],3, 'flowery-dot tights': flowery-dot tights,[White,:,White,None, Pink,:,Pink,White, Blue,:,Light blue,White, Yellow,:,Yellow,White, Black,:,Black,None],5, 'frilly knee-high socks': frilly knee-high socks,[Black,:,Black,White, Green,:,Green,White, Red,:,Red,White, Brown,:,Orange,White, Mint,:,Light blue,White, Pink,:,Pink,White, Purple,:,Purple,White, Yellow,:,Yellow,White],8, 'frilly socks': frilly socks,[White,:,White,None, Yellow,:,Yellow,White, Pink,:,Pink,White, Green,:,Green,White, Purple,:,Purple,White, Blue,:,Light blue,White],6, 'funny-face socks': funny-face socks,[Pink,:,Pink,Light blue, Blue,:,Blue,Green, Red,:,Red,Yellow, Green,:,Green,Blue, Black,:,Black,Gray],5, 'garter socks': garter socks,[Black,:,Black,None, White,:,White,None, Purple,:,Purple,None, Red,:,Red,None],4, 'geometric-print socks': geometric-print socks,[Yellow,:,Yellow,Colorful, Peacock blue,:,Light blue,Colorful, Purple,:,Purple,Colorful, Beige,:,Beige,Colorful, Pink,:,Pink,Colorful, Green,:,Green,Colorful],6, 'hand-knit socks': hand-knit socks,[Green,:,Green,None, Purple,:,Purple,None, Orange,:,Orange,None],3, 'holey socks': holey socks,[Blue,:,Blue,None, Navy blue,:,Blue,None, White,:,Beige,None],3, 'holey tights': holey tights,[Black,:,Black,None, Pink,:,Pink,None, Light blue,:,Light blue,None, Red,:,Red,None, Purple,:,Purple,None, Green,:,Green,None, Blue,:,Blue,None, Yellow,:,Yellow,None],8, 'kiddie socks': kiddie socks,[Red & light blue,:,Red,Light blue, Blue & orange,:,Blue,Orange, Lime & pink,:,Green,Pink, Yellow & purple,:,Yellow,Purple, Light blue & red,:,Light blue,Red, Purple & green,:,Purple,Green, Pink & yellow,:,Pink,Yellow, Black & gray,:,Black,Gray],8, 'Labelle socks': Labelle socks,[Twilight,:,Purple,None, Midnight,:,Black,None, Passion,:,Red,None, Ocean,:,Blue,None, Sunset,:,Yellow,None, Love,:,Pink,None],6, 'Labelle tights': Labelle tights,[Twilight,:,Purple,None, Midnight,:,Black,None, Passion,:,Red,None, Ocean,:,Blue,None, Sunset,:,Orange,None, Love,:,Pink,None],6, 'lace socks': lace socks,[White,:,White,None, Pink,:,Pink,White, Green,:,Green,White, Black,:,Black,White, Beige,:,Beige,White],5, 'layered socks': layered socks,[Purple,:,Gray,Purple, Blue,:,Gray,Blue, Yellow,:,Gray,Yellow, Green,:,Gray,Green, Red,:,Gray,Red, Orange,:,Gray,Orange],6, 'leg warmers': leg warmers,[Purple,:,Purple,None, Black,:,Black,None, Gray,:,Gray,None, Pink,:,Pink,None, Light purple,:,Purple,None, Blue,:,Blue,None],6, 'mixed-tweed socks': mixed-tweed socks,[Red,:,Red,None, Avocado,:,Green,None, Light blue,:,Light blue,None, Purple,:,Purple,None, Blue,:,Blue,None, Orange,:,Orange,None, Lime,:,Yellow,None, Pink,:,Beige,None],8, 'neon leggings': neon leggings,[Yellow,:,Yellow,Orange, Pink,:,Pink,Purple, Orange,:,Orange,Pink, Green,:,Green,Light blue, Purple,:,Purple,Blue],5, 'neon tights': neon tights,[Yellow,:,Yellow,Orange, Pink,:,Pink,Purple, Orange,:,Orange,Pink, Green,:,Green,Light blue, Purple,:,Purple,Blue],5, 'no-show socks': no-show socks,[Gray,:,Gray,Black, White,:,White,Red, Berry red,:,Red,Gray, Light blue,:,Light blue,White, Orange,:,Orange,Purple, Green,:,Green,Blue, Navy blue,:,Blue,Yellow, Yellow,:,Yellow,Light blue],8, 'Nook Inc. socks': Nook Inc. socks,[Yellow,:,Yellow,Orange],1, 'nordic socks': nordic socks,[Navy blue,:,Blue,Black, Ivory,:,Beige,Black, Red,:,Red,Black, Blue,:,Blue,Black, Gray,:,Gray,Black, Green,:,Green,Black, Light blue,:,Light blue,Black],7, 'patterned stockings': patterned stockings,[Black,:,Black,None, White,:,White,None],2, 'pom-pom socks': pom-pom socks,[Pink,:,Pink,White, Blue,:,Light blue,White, Green,:,Green,White, Orange,:,Orange,White, Purple,:,Purple,White],5, 'puckered socks': puckered socks,[Mustard,:,Orange,None, Red,:,Red,None, Blue,:,Blue,None, Green,:,Green,None, Purple,:,Purple,None],5, 'running tights': running tights,[Pink,:,Black,Pink, Yellow,:,Black,Yellow, Blue,:,Black,Blue, Green,:,Black,Green],4, 'semi-opaque socks': semi-opaque socks,[Green,:,Green,None, Red,:,Red,None, Blue,:,Blue,None, Navy blue,:,Purple,None, Purple,:,Pink,None, Camel,:,Yellow,None, Avocado,:,Green,None, Brown,:,Brown,None],8, 'semi-opaque tights': semi-opaque tights,[Brown,:,Orange,None, Yellow,:,Yellow,None, Green,:,Green,None, Purple,:,Purple,None, Blue,:,Blue,None, Pink,:,Pink,None, Red,:,Red,None, Yellow-green,:,Green,None],8, 'sequin leggings': sequin leggings,[Pink,:,Pink,None, Red,:,Red,None, Black,:,Black,None, Yellow,:,Yellow,None, White,:,White,None, Blue,:,Blue,None, Purple,:,Purple,None, Green,:,Green,None],8, 'sheer socks': sheer socks,[Blue,:,Blue,None, Berry red,:,Red,None, Brown,:,Brown,None, Green,:,Green,None, Olive,:,Green,None, Gray,:,Gray,None],6, 'simple knee-high socks': simple knee-high socks,[Pink,:,Pink,None, White,:,White,None, Red,:,Red,None, Blue,:,Light blue,None],4, 'simple-accent socks': simple-accent socks,[Navy blue,:,Blue,Red, Black,:,Black,White, White,:,White,Black, Gray,:,Gray,Light blue, Blue,:,Blue,Light blue, Orange,:,Orange,Yellow, Red,:,Red,Black, Pink,:,Pink,White],8, 'soccer socks': soccer socks,[Blue,:,Blue,White, Red,:,Red,White, Green,:,Green,White, Light blue,:,Light blue,White, Black,:,Black,White, Orange,:,Orange,White, White,:,White,Black],7, 'spider-web tights': spider-web tights,[Black,:,Black,None, White,:,White,None, Orange,:,Orange,None, Purple,:,Purple,None],4, 'stockings': stockings,[Black,:,Black,None, Gray,:,Gray,None, White,:,White,None, Brown,:,Brown,None, Beige,:,Beige,None],5, 'stretch leggings': stretch leggings,[Navy blue,:,Blue,None, Gray,:,Gray,None, Dark gray,:,Gray,None, White,:,White,None, Black,:,Black,None, Brown,:,Brown,None, Green,:,Green,None],7, 'striped socks': striped socks,[Monotone,:,Black,White, Light blue,:,Light blue,White, Green,:,Green,White, Yellow,:,Yellow,White, Orange,:,Orange,White, Red,:,Red,White, Purple,:,Purple,White, Blue,:,Blue,White],8, 'striped tights': striped tights,[Red,:,Red,Black, Gray,:,Gray,Black, Pink,:,Pink,Black, Light blue,:,Light blue,Black, Yellow,:,Yellow,Black, Purple,:,Purple,Black, Green,:,Green,Black, Orange,:,Orange,Black],8, 'tabi': tabi,[White,:,White,None, Black,:,Black,None, Navy blue,:,Blue,None],3, 'terry-cloth socks': terry-cloth socks,[Pink,:,Pink,White, Purple,:,Purple,White, Blue,:,Light blue,White, Green,:,Green,White, Beige,:,Beige,White, Red,:,Red,White, Gray,:,Gray,White],7, 'tube socks': tube socks,[Blue,:,White,Blue, Orange,:,White,Orange, Green,:,White,Green, Red,:,White,Red, Navy blue,:,Gray,Blue, Berry red,:,Gray,Red, Dark green,:,Gray,Green, Purple,:,Gray,Purple],8, 'ultra no-show socks': ultra no-show socks,[Blue,:,Blue,None, Pink,:,Pink,None, Brown,:,Brown,None, Olive,:,Green,None, Green,:,Green,None, Purple,:,Purple,None, Black,:,Black,None, White,:,White,None],8, 'vivid leggings': vivid leggings,[Light blue,:,Light blue,None, Purple,:,Purple,None, Red,:,Red,None, Pink,:,Pink,None, Blue,:,Blue,None, Yellow,:,Yellow,None, Green,:,Green,None, Orange,:,Orange,None],8, 'vivid socks': vivid socks,[Green,:,Green,None, Red,:,Red,None, Light blue,:,Light blue,None, Blue,:,Blue,None, Purple,:,Purple,None, Pink,:,Pink,None, Orange,:,Orange,None, Yellow,:,Yellow,None],8, 'vivid tights': vivid tights,[Light blue,:,Light blue,None, Purple,:,Purple,None, Red,:,Red,None, Pink,:,Pink,None, Blue,:,Blue,None, Yellow,:,Yellow,None, Green,:,Green,None, Orange,:,Orange,None],8, 'wave-print socks': wave-print socks,[Blue,:,Blue,Light blue, Brown,:,Brown,Beige, Purple,:,Purple,Pink, Green,:,Green,None, Gray,:,Black,Gray],5}

Notice:This print of the all_socks dictionary contains each sock type, all of the variations under each type, all of the colors of the variations, and the number of variations a sock type has. 

### Task 2: Which Sock Has the Most variations 
For this task I used a for loop to iterate through all_socks and a list to store the socks with the most variaitons. Here is the code for this task: 
```
list_most_variations = []
highest_count = 0
for name in all_socks:
    if all_socks[name].count_variations() > highest_count: 
        highest_count = all_socks[name].count_variations()
        list_most_variations.clear()
        list_most_variations.append(name)
    elif all_socks[name].count_variations() == highest_count: 
        list_most_variations.append(name)
print()
print(str(list_most_variations) + " all have the " + str(highest_count) + " variations, which is the highest number of variations.")
```
The code has two parts. The first part of the code checks what the highest number of variations a sock type can have is. It does this by comparing the variations of each sock to a highest count variable. If the sock type has a higher number than the stored number in the variable highest_count, then the numbeer is replaced and the code continues to iterat through the rest of all_socks to see if there is an even higher number of variations. Once it has found the highest number of variations, it iterates through all_socks one more time to add the names of the sock types with 8 variations (the highest number of variations) to a list called list_most_variations. 

Here is my answer to task 2: 
['argyle crew socks', 'color-blocked socks', 'frilly knee-high socks', 'holey tights', 'kiddie socks', 'mixed-tweed socks', 'no-show socks', 'semi-opaque socks', 'semi-opaque tights', 'sequin leggings', 'simple-accent socks', 'striped socks', 'striped tights', 'tube socks', 'ultra no-show socks', 'vivid leggings', 'vivid socks', 'vivid tights'] all have the 8 variations, which is the highest number of variations.

### Task 3: Counting Colors
For this task I used a dictionary with keys of each color and values would represent to count of that color. Here is the code for this task: 
```
dic_color_count = {}
for sock in all_socks: 
    for variation in all_socks[sock].variation:   
        color1 = variation.getColor1()
        color2 = variation.getColor2()
        if color1 not in dic_color_count: 
            dic_color_count[color1] = 1
        elif color1 in dic_color_count: 
            dic_color_count[color1] += 1

        if color2 not in dic_color_count: 
            dic_color_count[color2] = 1
        elif color2 in dic_color_count: 
            dic_color_count[color2] += 1
print()
print(dic_color_count)
```

Notice how it seperates color 1 and color 2 for all of the socks. This is necessary because the colors are seperated in the variations class, so I have to do the process for both color slots. How this code works is that it gets the colors and checks if the dictionary dic_color_count already has a key for that color and if it doesn't it creates a key and makes the value one. If it already has a key then it ads 1 to the value. It does it for both color 1 and 2 but it can use the same dictionary because it stores the colors in new variables color1 and color2. 

Here is the printed dictionary: 
{'Pink': 41, 'Red': 39, 'Green': 50, 'Light blue': 33, 'Orange': 27, 'Purple': 37, 'Blue': 47, 'Yellow': 33, 'Beige': 15, None: 178, 'White': 85, 'Black': 59, 'Brown': 11, 'Gray': 31, 'Colorful': 14}

Notice how my output has a none count in it. This is because some of the socks have both the same color1 and color2, but those colors do not get double counted in color1 and color2 are the same. So there is this line of code in my variaions class that takes care of that: 
```
if color_2 == color_1: 
        color_2 = None
```
So if the color1 and color2 are the same color2 gets set to none, so in the dictionary that none value also gets counted and it has a value of 178 meaning that 178 of the socks have the same color1 and color2. 

### Task 4
This lab was really fun and really eye opening. It was my first practice with classes since last year in CompSci 2 and my first practice of classes in Python. There were a lot of little bumps in the way with things like syntax and missing letters and misspelled variables. For example my variations class took a while to work because there was a little syntax error that caused color counts to be stored improperly which impacted the color count in task 3. But after a little bit of tweaking with Mr. Lee, I got it to work. Mr. Lee was my collaborator for most of the tasks since this was my first practice with classes and I needed a a lot of help along the way. Even though the process was a little crazy and mistake filled, it was incredibly fulfilling when my code finally worked correctly. 

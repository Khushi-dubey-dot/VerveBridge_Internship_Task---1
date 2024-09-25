import pandas as pd
import requests
from bs4 import BeautifulSoup
Product_name = []
Prices = []
Description = []
Reviews = []


for i in range(2,12):
  url = "https://www.flipkart.com/search?q=mobiles%20under%2050000&otracker=search&otracker1=search&marketplace=FLIPKART&as-show=on&as="+str(i)

r = requests.get(url)
   #print(r)

soup = BeautifulSoup(r.text, "lxml")
box = soup.find("div",class_ = "DOjaWf gdgoEp")

names = box.find_all("div",class_ ="_KzD1HZ")

for i in names:
    name = i.text
    Product_name.append(name)

# print(Product_name) 

 prices = box.find_all("div",class_ = "Nx9bj _4b5DiR")

 for i in prices:
     name = i.text
     Prices.append(name)
# print(Prices)

     desc = box.find_all("ul",class_ = "yKfJKb)

     for i in desc:
         name = i.text
         Description.append(name)

 # print(Description)

 reviews = box.find_all("div",class_ = "XQDdHH")

 for i in reviews:
     name = i.text
     Reviews.append(name)

     print(Reviews)

df = pd.DataFrame({"Product name":Product_name,"Prices":Prices,"Description":Description,"Reviews":Reviews})

df.to_csv("flipkart_mobiles_under_50000.csv") #print(soup)


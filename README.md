# Pandas_Homework

I've been assigned the task of analyzing the data for their most recent fantasy game Heroes of Pymoli.

Like many others in its genre, the game is free-to-play, but players are encouraged to purchase optional items that enhance their playing experience. As a first task, the company would like you to generate a report that breaks down the game's purchasing data into meaningful insights.

My final report includes each of the following:

# Name at least three observable trends in the data
#Among the 576 total players, 84.03% of players are male
#The age group spending the most money is 20-24 years old (44.79%) while 15-19 and 25-29 make up the top three.  
#Females, while smaller in number, outspend males, on average ($4.47 v $4.07, respectively)
#Final Critic is the most popular item in terms of purchase count and purchase value



### Player Countcd


* Total Number of Players 576

### Purchasing Analysis (Total)

* Number of Unique Items 179
* Average Purchase Price $3.05
* Total Number of Purchases 780
* Total Revenue $2379.77

### Gender Demographics

* Percentage and Count of Male Players 84.03%; 484
* Percentage and Count of Female Players 14.06%; 81
* Percentage and Count of Other / Non-Disclosed 1.91%; 11

### Purchasing Analysis (Gender)

  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Gender

### Age Demographics

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.)
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Average Purchase Total per Person by Age Group

### Top Spenders

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value

### Most Popular Items

* Identify the 5 most popular items by purchase count, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

### Most Profitable Items

* Identify the 5 most profitable items by total purchase value, then list (in a table):
  * Item ID
  * Item Name
  * Purchase Count
  * Item Price
  * Total Purchase Value

As final considerations:

* You must use the Pandas Library and the Jupyter Notebook.
* You must submit a link to your Jupyter Notebook with the viewable Data Frames.
* You must include a written description of three observable trends based on the data.
* See [Example Solution](HeroesOfPymoli/HeroesOfPymoli_starter.ipynb) for a reference on expected format.


My Work:

#Display the total number of players
total_players = len(purchase_data_df["SN"].value_counts())
player_count = pd.DataFrame({"Total Players": [total_players]})
player_count


#Calculate the number of unique items
number_of_unique_items = len(purchase_data_df["Item ID"].unique())

#Calculate the average price
average_price = purchase_data_df["Price"].mean()

#Calculate the total number of purchases
total_purchases = purchase_data_df["Purchase ID"].count()

#Calculate the Total Revenue
total_revenue = purchase_data_df["Price"].sum()

#Create a summary frame to hold the results
summary_df = pd.DataFrame({"Number of Unique Items":[number_of_unique_items], 
                               "Average Purchase Price":[average_price], 
                               "Total Number of Purchases":[total_purchases],
                                "Total Revenue": [total_revenue]})

# Format using currency and decimals
summary_df.style.format({"Average Purchase Price": "${:,.2f}",
                                    "Total Number of Purchases": "${:,.2f}",
                                    "Total Revenue": "${:,.2f}"})





#Group calculations by the "Gender" column
grouped_by_gender = purchase_data_df.groupby("Gender")

#Calculate the unique SN by gender
players_by_gender = grouped_by_gender["SN"].nunique()

#Calculate the percentage of players by gender
percentage_players_gender = players_by_gender / total_players * 100

#Calculate the gender count and percentage of players
gender_demographics_df = pd.DataFrame({"Percentage of Players": percentage_players_gender, "Total Count": players_by_gender})
gender_demographics_df

#Round the percentage column to two decimal points
gender_demographics_df.style.format({"Percentage of Players":"{:,.2f}%"})




#Calculate the purchase count by gender
purchase_count = grouped_by_gender["Purchase ID"].count()

#Calculate the average purchase price by gender
average_purchase_price = grouped_by_gender["Price"].mean()

#Calculate the total purchase price by gender
total_purchase_price = grouped_by_gender["Price"].sum()

#Calculate the average purchase total per person by gender
average_per_person_total = total_purchase_price / players_by_gender


#Create a summary data frame with obtained values 
purchases_by_gender_df = pd.DataFrame({"Purchase Count": purchase_count, 
                                    "Average Purchase Price": average_purchase_price,
                                    "Total Purchase Price":total_purchase_price,
                                    "Average Purchase Total per Person": average_per_person_total})
#Format using currency and decimals
purchases_by_gender_df.style.format({"Average Purchase Price": "${:,.2f}",
                                    "Total Purchase Price": "${:,.2f}",
                                    "Average Purchase Total per Person": "${:,.2f}"})




#Create bins by age for the purchase data
age_bins = [0, 9.99, 14.99, 19.99, 24.99, 29.99, 34.99, 39.99, 200]
age_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

purchase_data_df["Age Group"] = pd.cut(purchase_data_df["Age"], age_bins, labels=age_names)

#Group calculations by the "Age Group" column
grouped_by_age = purchase_data_df.groupby("Age Group")

#Calculate the unique SN by age group
players_by_age = grouped_by_age["SN"].nunique()

#Calculate the percentage of players by age
percentage_players_age = players_by_age / total_players * 100

#Calculate the age count and percentage of players
age_demographics_df = pd.DataFrame({"Percentage of Players": percentage_players_age, "Total Count": players_by_age})

#Round the percentage column to two decimal points
age_demographics_df.style.format({"Percentage of Players":"{:,.2f}%"})




#Create bins by age for the purchase data
age_bins = [0, 9.99, 14.99, 19.99, 24.99, 29.99, 34.99, 39.99, 200]
age_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

purchase_data_df["Age Group"] = pd.cut(purchase_data_df["Age"], age_bins, labels=age_names)

grouped_by_age = purchase_data_df.groupby("Age Group")

#Calculate the unique SN by age
players_by_age = grouped_by_age["SN"].nunique()

#Calculate the purchase count by age group
purchase_count_age = grouped_by_age["Purchase ID"].count()

#Calculate the average purchase price by gender
average_purchase_price_age = grouped_by_age["Price"].mean()

#Calculate the total purchase price by gender
total_purchase_price_age = grouped_by_age["Price"].sum()

#Calculate the average purchase total per person by gender
average_per_person_total_age = total_purchase_price_age / players_by_age


#Create a summary data frame with obtained values 
purchases_by_age_df = pd.DataFrame({"Purchase Count": purchase_count_age, 
                                    "Average Purchase Price": average_purchase_price_age,
                                    "Total Purchase Price":total_purchase_price_age,
                                    "Average Purchase Total per Person": average_per_person_total_age})

#Format using currency and decimals
purchases_by_age_df.style.format({"Average Purchase Price": "${:,.2f}",
                                    "Total Purchase Price": "${:,.2f}",
                                    "Average Purchase Total per Person": "${:,.2f}"})


#Group calculations by the Screen Name column
grouped_by_screen_name = purchase_data_df.groupby("SN")

#Calculate the total number of purchases by SN
purchase_count_spender = grouped_by_screen_name["Purchase ID"].count()

#Calculate the average price
average_purchase_price_spender = grouped_by_screen_name["Price"].mean()

#Calculate the Total Purchases by SN
total_purchases_spender = grouped_by_screen_name["Price"].sum()

#Create a summary frame to hold the results
top_spender_summary_df = pd.DataFrame({"Purchase Count":[purchase_count_spender], 
                               "Average Purchase Price":[average_purchase_price_spender], 
                               "Total Purchase Value": [total_purchases_spender]})

#Format using currency and decimals
summary_df.style.format({"Average Purchase Price": "${:,.2f}",
                        "Total Purchase Value": "${:,.2f}"})



#Group calculations by the Screen Name column
grouped_by_screen_name = purchase_data_df.groupby("SN")

#Calculate the total number of purchases by SN
purchase_count_spender = grouped_by_screen_name["Purchase ID"].count()

#Calculate the average price
average_purchase_price_spender = grouped_by_screen_name["Price"].mean()

#Calculate the Total Purchases by SN
total_purchases_spender = grouped_by_screen_name["Price"].sum()

#Create a summary frame to hold the results
spender_summary = pd.DataFrame({"Purchase Count":purchase_count_spender, 
                               "Average Purchase Price":average_purchase_price_spender, 
                               "Total Purchase Value": total_purchases_spender})

#Format to sort total purchase value in desceding order
descending_spenders = spender_summary.sort_values(["Total Purchase Value"], ascending=False)

#Format using currency and decimals
descending_spenders.style.format({"Average Purchase Price": "${:,.2f}",
                        "Total Purchase Value": "${:,.2f}"})



#Create a most popular items data frame
popular_items = purchase_data_df[["Item ID", "Item Name", "Price"]]

#Group the Item ID and Item Name
item_attributes = popular_items.groupby(["Item ID", "Item Name"])

#Calculate the purchase count
item_purchase_count = item_attributes["Price"].count()

#Calculate the average item price
average_item_price = item_attributes["Price"].mean()

#Calculate the total purchase value
total_purchase_value = item_attributes["Price"].sum()

#Create a summary frame to hold the results
item_summary = pd.DataFrame({"Purchase Count":item_purchase_count, 
                               "Average Item Price":average_item_price, 
                               "Total Purchase Value": total_purchase_value})

#Format to sort purchase count column in descending order
descending_items = item_summary.sort_values(["Total Purchase Value"], ascending=False)

#Format using currency and decimals
descending_items.style.format({"Average Item Price": "${:,.2f}",
                                "Total Purchase Value": "${:,.2f}"})

#Format to sort purchase count column in descending order
descending_items = item_summary.sort_values(["Total Purchase Value"], ascending=False)

#Format using currency and decimals
descending_items.style.format({"Average Item Price": "${:,.2f}",
                                "Total Purchase Value": "${:,.2f}"})

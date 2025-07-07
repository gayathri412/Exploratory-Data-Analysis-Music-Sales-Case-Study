# Exploratory-Data-Analysis-Music-Sales-Case-Study
 Objective: To analyze a dataset containing music sales and understand key insights such as: 
 Top-selling genres, albums, and artists  
 Trends over time  
 Geographical impact on sales  
 Relationships between different factors like genre and sales

Dataset Overview
Assume the dataset has the following columns:
Column Name	Description
InvoiceID	Unique ID for each sale
CustomerID	Unique ID for each customer
Country	Country where the purchase was made
InvoiceDate	Date of the transaction
TrackID	ID of the song/track
TrackName	Name of the track
Genre	Genre of the music
Artist	Artist name
Album	Album name
UnitPrice	Price of one unit
Quantity	Quantity sold
Total	Total = UnitPrice × Quantity

🔍 1. Data Preprocessing
✅ Tasks:
Check for missing/null values

Convert InvoiceDate to datetime

Create new features: Year, Month, Weekday

Ensure UnitPrice, Quantity, and Total are numeric

python
Copy
Edit
df['InvoiceDate'] = pd.to_datetime(df['InvoiceDate'])
df['Year'] = df['InvoiceDate'].dt.year
df['Month'] = df['InvoiceDate'].dt.month
df['Weekday'] = df['InvoiceDate'].dt.day_name()
📊 2. Descriptive Statistics
🔸 Summary
python
Copy
Edit
df.describe()
Average sale per transaction

Max quantity ordered

Revenue distribution

📈 3. Sales Over Time
🎯 Objective:
Understand trends in music sales over months/years.

python
Copy
Edit
monthly_sales = df.groupby(['Year', 'Month'])['Total'].sum().reset_index()
sns.lineplot(x='Month', y='Total', hue='Year', data=monthly_sales)
Seasonality patterns (e.g., holidays?)

Peak sales months

🎼 4. Top Genres, Artists, and Albums
🔹 Top Genres by Revenue
python
Copy
Edit
df.groupby('Genre')['Total'].sum().sort_values(ascending=False).head(10)
🔹 Top Artists
python
Copy
Edit
df.groupby('Artist')['Total'].sum().sort_values(ascending=False).head(10)
🔹 Top Albums
python
Copy
Edit
df.groupby('Album')['Total'].sum().sort_values(ascending=False).head(10)
Use bar charts for visualizing.

🌍 5. Geographical Analysis
🔹 Sales by Country
python
Copy
Edit
df.groupby('Country')['Total'].sum().sort_values(ascending=False).plot(kind='bar')
Identify countries contributing most to sales

Check if specific genres perform well in certain countries

🧑‍🤝‍🧑 6. Customer Behavior
🔹 Repeat Customers
Most loyal customers (by purchase count or total value)

python
Copy
Edit
df.groupby('CustomerID')['Total'].sum().sort_values(ascending=False).head(10)
🔹 Average Basket Size
python
Copy
Edit
avg_basket = df.groupby('InvoiceID')['Total'].sum().mean()
🔗 7. Correlation Analysis
Between Quantity, UnitPrice, Total

python
Copy
Edit
df[['Quantity', 'UnitPrice', 'Total']].corr()
Visualize with a heatmap.

📌 8. Key Insights
Which genre brings the most revenue?

Are sales seasonal (e.g., higher in December)?

Which country contributes the most?

Who are the top-performing artists and albums?

Is there a strong correlation between price and quantity?

📑 9. Recommendations
Promote top genres in high-revenue countries

Launch marketing campaigns during peak sales months

Upsell albums from top artists to high-spending customers

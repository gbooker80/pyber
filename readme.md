
# Pyber Ride Sharing

<h3>Analysis</h3>

-Rural Fares tend to have higher average fares but make up a small proportion of overall revenue.

-Drivers are heavily centered in urban areas and this may have a negative effect on average fares in this area.

-Despite the lower average fares, urban areas account for 63% of total revenue.


```python
import pandas as pd
from matplotlib import pyplot as plt
import seaborn as sns

city_data = "city_data.csv"
city_data  = pd.read_csv(city_data)
ride_data = "ride_data.csv"
ride_data = pd.read_csv(ride_data)

combined_data = pd.merge(ride_data, city_data, how="left", on=["city","city"])

combined_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>



<h3>Bubble Plot of Ride Sharing Data</h3>


```python
urban_rides = combined_data[combined_data["type"] == "Urban"]
suburban_rides = combined_data[combined_data["type"] == "Suburban"]
rural_rides = combined_data[combined_data["type"] == "Rural"]

urban_ride_total = urban_cities.groupby(["city"]).count()["ride_id"]
urban_ride_avg = urban_cities.groupby(["city"]).mean()["fare"]
urban_driver = urban_cities.groupby(["city"]).mean()["driver_count"]

suburban_ride_total = suburban_cities.groupby(["city"]).count()["ride_id"]
suburban_ride_avg = suburban_cities.groupby(["city"]).mean()["fare"]
suburban_driver = suburban_cities.groupby(["city"]).mean()["driver_count"]

rural_ride_total = rural_cities.groupby(["city"]).count()["ride_id"]
rural_ride_avg = rural_cities.groupby(["city"]).mean()["fare"]
rural_driver = rural_cities.groupby(["city"]).mean()["driver_count"]
```


```python
plt.scatter(urban_ride_total,
            urban_ride_avg,
            s=15*urban_driver, c="lightskyblue",
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Urban")

plt.scatter(suburban_ride_total,
            suburban_ride_avg,
            s=15*suburban_driver, c="gold",
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Suburban")

plt.scatter(rural_ride_total, 
            rural_ride_avg, 
            s=15*rural_driver_count, c="lightcoral", 
            edgecolor="black", linewidths=1, marker="o", 
            alpha=0.8, label="Rural")

plt.title("Pyber Ride Sharing Data (2016)")
plt.ylabel("Average Fare ($)")
plt.xlabel("Total Number of Rides (Per City)")
plt.xlim((-1,38))
plt.grid(True)

plt.legend(fontsize="small", mode="Expanded",
                  numpoints=1, scatterpoints=1,
                  loc="best", title="City Types",
                  labelspacing=1.2)

plt.show()
```


![png](output_6_0.png)


<h3>Total Fares by City Type</h3>


```python
fare_percentage = 100 * combined_data.groupby(["type"]).sum()["fare"] / combined_data["fare"].sum()

plt.pie(fare_percentage,
        labels=["Rural", "Suburban", "Urban"],
        colors=["lightcoral", "gold", "lightskyblue"],
        explode=[0, 0, 0.1],
        autopct='%1.1f%%',
        shadow=True, startangle=120)
plt.title("Percentage of Fares by City Type")

plt.show()
```


![png](output_8_0.png)


<h3>Total Rides by City Type</h3>


```python
ride_percentage = 100 * combined_data.groupby(["type"]).count()["ride_id"] / combined_data["ride_id"].count()

plt.pie(ride_percentage,
        labels=["Rural", "Suburban", "Urban"],
        colors=["lightcoral", "gold", "lightskyblue"],
        explode=[0, 0, 0.1],
        autopct='%1.1f%%',
        shadow=True, startangle=120)
plt.title("Percentage of Fares by City Type")

plt.show()
```


![png](output_10_0.png)


<h3>Total Drivers by City Type</h3>


```python
driver_percentage = 100 * city_data.groupby(["type"]).sum()["driver_count"] / city_data["driver_count"].sum()

plt.pie(driver_percentage,
        labels=["Rural", "Suburban", "Urban"],
        colors=["lightcoral", "gold", "lightskyblue"],
        explode=[0, 0, 0.1],
        autopct='%1.1f%%',
        shadow=True, startangle=120)
plt.title("Percentage of Fares by City Type")

plt.show()
```


![png](output_12_0.png)


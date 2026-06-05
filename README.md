
# Introduction
---
Lets say I wanted to open a restaraunt, particularly in Honolulu. Then I would want to prepare myself and gain insights into what makes a succesful business in the area. This project will analyse a dataset of Google reviews from Hawaii scraped by the authors of these papers https://aclanthology.org/2022.acl-long.426.pdf, https://arxiv.org/pdf/2207.00422. I want to find out what it takes to run a succesful restaraunt in Honolulu, and my first related question when presented with this data set is if there is a correlation between a restaraunts average rating, and their number of reviews. I'm interested in the number of reviews because more reviews imply more business. There are 2 original data frames, one focused on businesses with 21507 rows and 15 columns, and one focues on individual reviews with 1504347 rows and 8 columns
## reviews

| Column | Description |
| :--- | :--- |
| `user_id` | ID of the reviewer |
| `name` | name of the reviewer |
| `time` | time of the review (unix time) |
| `rating` | rating of the business |
| `text` | text of the review |
| `pics` | pictures of the review |
| `resp` | business response to the review including unix time and text of the response |
| `gmap_id` | ID of the business |

## businesses

| Column | Description |
| :--- | :--- |
| `name` | name of the business |
| `address` | address of the business |
| `gmap_id` | ID of the business |
| `description` | description of the business |
| `latitude` | latitude of the business |
| `longitude` | longitude of the business |
| `category` | category of the business |
| `avg_rating` | average rating of the business |
| `num_of_reviews` | number of reviews |
| `price` | price of the business |
| `hours` | open hours |
| `MISC` | MISC information |
| `state` | the current status of the business (e.g., permanently closed) |
| `relative_results` | relative businesses recommended by Google |
| `url` | URL of the business |

---

# Data Cleaning and Exploratory Data Analysis
- The data is collected from all of Hawaii. Since I want to open a restaraunt in Honolulu, the first thing I'll do is focus the businesses dataset on the most prominent Honolulu zip codes.

| Zip Code | Area |
| :--- | :--- |
| `96815` | Waikiki, Kapahulu |
| `96813` | Downtown Honolulu, Nuuanu, Kakaako (West) |
| `96814` | Ala Moana, Kakaako (East), Makiki (Lower) |
| `96816` | Kaimuki, Kahala, Waialae, Palolo |
| `96822` | Manoa, Makiki (Upper), Tantalus |
| `96825` | Hawaii Kai |
- The data is now focused on Honolulu, however it still contains all sorts of businesses. Now I'll keep only businesses categorized as restaraunts.
- I make a dedicated column for zipcodes because it will help in seeing diferences between the zipcodes
- Since the state column is full of diferent entries because each store has a different schedule, I'll make a new column that just says if a 
store is open, closed, or temporarily closed
- I changed the None values into np.nan values for consistency
- I wanted to check for duplicate rows, so I checked the gmap_id value counts. I realized there were some duplicate rows so I removed them
- In order to give the do analysis of the "price" column, I made the strings "$"..."$$$$" into 1...4
- My cleaned df restaurants only has 1055 rows compared to the original df's 21507 rows

<div style="overflow-x: auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>name</th>
      <th>address</th>
      <th>gmap_id</th>
      <th>description</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>category</th>
      <th>avg_rating</th>
      <th>num_of_reviews</th>
      <th>price</th>
      <th>hours</th>
      <th>MISC</th>
      <th>state</th>
      <th>relative_results</th>
      <th>url</th>
      <th>zip_code</th>
      <th>states_simple</th>
      <th>price_vals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Akasatana Ramen Kyoto</td>
      <td>Akasatana Ramen Kyoto, 1450 Ala Moana Blvd, Honolu...</td>
      <td>0x7c006df045b01715:0xe945c308688e1a46</td>
      <td>nan</td>
      <td>21.290463199999998</td>
      <td>-157.84373</td>
      <td>['Ramen restaurant']</td>
      <td>5.0</td>
      <td>1</td>
      <td>nan</td>
      <td>[array(['Thursday', '11AM–8:30PM'], dtype=object)\n...</td>
      <td>{'Accessibility': None, 'Amenities': None, 'Planni...</td>
      <td>Closed ⋅ Opens 11AM</td>
      <td>['0x7c006df018f6177d:0x9beb6db40fadcb2'\n '0x7c006d...</td>
      <td>https://www.google.com/maps/place//data=!4m2!3m1!1...</td>
      <td>96814</td>
      <td>Open</td>
      <td>nan</td>
    </tr>
    <tr>
      <td>Tucker &amp; Bevvy Breakfast</td>
      <td>Tucker &amp; Bevvy Breakfast, 449 Kapahulu Ave, Honolu...</td>
      <td>0x7c007278edb2a865:0x4ed1c3d61fda94aa</td>
      <td>nan</td>
      <td>21.2717638</td>
      <td>-157.8223992</td>
      <td>['Fast food restaurant' 'Restaurant']</td>
      <td>4.2</td>
      <td>57</td>
      <td>nan</td>
      <td>[array(['Wednesday', '6AM–7:30PM'], dtype=object)\n...</td>
      <td>{'Accessibility': array(['Wheelchair accessible en...</td>
      <td>Open ⋅ Closes 7:30PM</td>
      <td>['0x7c0072776fb74005:0x18806e32e561ef36'\n '0x7c007...</td>
      <td>https://www.google.com/maps/place//data=!4m2!3m1!1...</td>
      <td>96815</td>
      <td>Open</td>
      <td>nan</td>
    </tr>
    <tr>
      <td>Infinitea Cafe Llc</td>
      <td>Infinitea Cafe Llc, 808 Sheridan St, Honolulu, HI ...</td>
      <td>0x7c006deee2792595:0x1233c8d3b2862bb</td>
      <td>nan</td>
      <td>21.2968442</td>
      <td>-157.84259409999999</td>
      <td>['Restaurant' 'Cafe']</td>
      <td>4.3</td>
      <td>33</td>
      <td>$$</td>
      <td>[array(['Wednesday', '10AM–9PM'], dtype=object)\n a...</td>
      <td>{'Accessibility': None, 'Amenities': None, 'Planni...</td>
      <td>Temporarily closed</td>
      <td>['0x7c006e85fd95f1d3:0x5f95ded24b8a8dff'\n '0x7c006...</td>
      <td>https://www.google.com/maps/place//data=!4m2!3m1!1...</td>
      <td>96814</td>
      <td>Temporarily closed</td>
      <td>2.0</td>
    </tr>
    <tr>
      <td>DoorDash Hawaii</td>
      <td>DoorDash Hawaii, 1500 Kapiolani Blvd #207, Honolul...</td>
      <td>0x7c006daf797e55c3:0xfb83fa85ff58477b</td>
      <td>nan</td>
      <td>21.293001</td>
      <td>-157.8415895</td>
      <td>['Event technology service' 'Corporate office' 'De...</td>
      <td>1.8</td>
      <td>77</td>
      <td>nan</td>
      <td>[array(['Tuesday', '10:45AM–6:45PM'], dtype=object...</td>
      <td>nan</td>
      <td>Closed ⋅ Opens 10:45AM</td>
      <td>['0x7c0014db1986e907:0x9e18bb4d51795f1a'\n '0x7c006...</td>
      <td>https://www.google.com/maps/place//data=!4m2!3m1!1...</td>
      <td>96814</td>
      <td>Open</td>
      <td>nan</td>
    </tr>
    <tr>
      <td>Eat On Time</td>
      <td>Eat On Time, 1296 S Beretania St unit106, Honolulu...</td>
      <td>0x7c006d36073bb95f:0xe5527438ba899941</td>
      <td>nan</td>
      <td>21.301271699999997</td>
      <td>-157.8410428</td>
      <td>['Chinese restaurant' 'Asian restaurant' 'Chinese ...</td>
      <td>4.0</td>
      <td>17</td>
      <td>nan</td>
      <td>[array(['Monday', '10AM–9PM'], dtype=object)\n arra...</td>
      <td>{'Accessibility': None, 'Amenities': array(['Good ...</td>
      <td>Open ⋅ Closes 9PM</td>
      <td>nan</td>
      <td>https://www.google.com/maps/place//data=!4m2!3m1!1...</td>
      <td>96814</td>
      <td>Open</td>
      <td>nan</td>
    </tr>
  </tbody>
</table>
</div>

# Unvariate Analysis
This plot is displaying a histogram showing the distribution of the average ratings for restaraunts in my area of focus. The distribution is skewed to the right and it reveals how most ratings are pretty close to the mean of approximately 4.2 stars, which is pretty high considering the maximum rating is 5.
<iframe
  src="assets/UA_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



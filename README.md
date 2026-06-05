# Honolulu Restaurant Project 🌺

# Introduction
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
# Bivariate Analysis
Bivariate Analysis - As I've said before, I suspect there is a correlation between average rating and the number of reviews for a restaraunt. Before I test for correlation I wanted to see the distribution between the two variables. I uses logscale again to fit in num_of_reviews. Unfourtunately the graph doesent clearly reveal a relationship between the two variables. The average ratings seem to hover around the mean of 4.2 across the board. It even seems avg rating could drop slightly the more reviews a establishment has, which goes against my what I thought.
<iframe
  src="assets/BA_plot1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
A more promising relationship seems to be the one between price and the number of reviews. It seems that the number of reviews gradually increases until the '$$$' mark and then slightly drops off. This could mean that restaraunts with price '$$$' have the most reviews, and potenitally the most business.
<iframe
  src="assets/BA_plot2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
# Interesting Aggregates
Interesting Aggregates - In order to see if some zipcodes are good for business, or even if some are bad for it, I wanted to check the percentage of open restaurants in each zipcode im considering for my business. Honestly, I expected the percentages to all be pretty similar, and for the most part they were, however zipcode 96815 is clearly performing poorly. This is interesting because thats the famous tourist area of Waikiki. 96825 had the highest open percentage, and that area is Hawaii Kai which is an upscale neighborhood area in east Honolulu. These insights will be helpful to decide the area I should open my restaraunt. Particularly if I want to open in Waikiki, I will have to thoroughly analyze what makes a succesful restaraunt there because the closure rate is high there. Overall, the mean open percentage in my area of focus is around 72.64% which is promising.
<bound method DataFrame.to_html of states_simple   Open  Permanently closed  Temporarily closed  open_percentage
zip_code                                                                     
96813           84.0                23.0                 4.0            75.68
96814          148.0                52.0                12.0            69.81
96815          121.0                58.0                30.0            57.89
96816           84.0                27.0                 2.0            74.34
96822           25.0                 4.0                 3.0            78.12
96825           28.0                 7.0                 0.0            80.00>

# Assesment of Missingness
## NMAR Analysis
I suspect that the 'hours' column has NMAR data. My reasoning is that businesses that are small scale, unregulated, unpermited, or failing are more likely to have speratic schedules that are more dictated by the convinience of the owner. For example the google review page for a sidehustle like a roadside fruit stand would omit hours because the owner only operates when they have free time. Data that could be collected to explain the missingness would be legal registration details like wether a business is an LLC or sole propritorship as well as if they have the necessary permits required for their category of business.
## Missingness Dependency
To anylize missingness in businesses I will conduct missingness dependency test on the columns price and num_of_reviews
**Null Hypothesis** - The missingness of price does not depend on the number of reviews
**Alternate Hypothesis** - The missingness of price does depend on the number of reviews 
**Test Statistic** - Difference of Means
**Significance level** - 0.05
After running the test I found a difference in means of 219.81 and a p value of 0.0000, therefore we can reject the null and say the missingness of price does depend on the number of reviews
Next I wanted to test wether the missingness of Price depended on wether the gmap id had an a in it.
**Null Hypothesis** - The missingness of price does not depend on wether the gmap id has an a in it
**Alternate Hypothesis** - The missingness of price does depend on wether the gmap id has an a in it
**Test Statistic** - Difference of Proportion
**Significance level** - 0.05
The test revealed a a difference in proportion of 0.004413 and a p value of 0.5060, therefore we fail to reject the null that the missingness of price doesent depend on wether the gmap id has an a in it.
<iframe
  src="assets/Missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/Missing2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Hypothesis Testing
When exploring the data I found the most promising relationship lie within the distribution of review counts by price tier. I've decided to conduct a test as to wether there is a positive correlation between price and the number of reviews a restaraunt has in my area of focus. Using the number of reviews as a measure of success for a restaurant, this could give insight into wether higher prices can contribute to the success of my business.
- **Null Hypothesis** - There is no correlation between price tier and the number of reviews for a restaurant
- **Alternate Hypothesis** - There is a correlation between price tier and the number of reviews for a restaurant
- **Test Statistic** - Absolute Pearson Correlation Coefficient
- **Significance** - 0.05
I ran the test by dropping rows without a price and then used the price_vals column to measure the prices relationship to review counts. I shuffled the review counts 1000 times to find 1000 of the abs pearson correlations. Because the P-value is 0.0110 which is less than 0.05, I reject the null hypothesis that there is no correlation between price tier and the number of reviews for a restaurant. However, it's important to note that the correlation coefficient is very small, only 0.0975. This could be due to the patern noted earlier where the number of reviews seems to rise untill '$$$' and then drops off at '$$$$', but it's important to acknowldge that such a low correlation could suggest that price level is not a great predictor for the number of reviews a restaurant has.
<iframe
  src="assets/HT.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
# Framing a Prediction Problem
Framing a prediction problem - I would like to be able to predict wether a restaurant is at risk of closing because understanding what factors could lead a restaurant to failure can help me avoid them. This problem is a binary classification problem because I will be predicting if a restaurant is open(0) or closed(1). The response variable will be the restaurants state, i.e wether the business is open or not (In this problem "temporarily closed" will be considered open). I chose to predict this variable because it is the precursor to all success in a business, the place could be killing it on all metrics but that doesen't matter if they had to shut down. I will be evaluating my model with F1 score. This is because it has already been established previously that the majority of restaurants in my focus area are open (around 73%) so an insufficent model could easily just predict every restaurant is open to get a decent accuracy. Since F1 is the harmonic mean of precision and recall, it will be able to penalize both false positives and false negatives evenly, and this can prevent the aformentioned sloppy model. Data to use in the model must be reasonable at the time of prediction. This means that I'll be able to use data like price, num ratings, avg ratings, coordinates, and category because they are present when its business as usual. Data I cant use includes a reviews text and pictures because this may reveal a business is already in the process of permanently closing.
# Baseline Model
My baseline model is a binary logistic regression classifier that predicts whether a restaurant is at risk of closing down in my focus area. The target variable was made to be the state of a restaurant with closed being 1, and open being 0. The data was divided into training and testing data in order to evaluate the models ability to generalize on unseen data. The models first feature was price which was an ordial, it originally categorically represented price with strings '$'...'$$$$' but I tranformed it with an ordianl encoder so the model can understand the higherarchy of the price tiers mathematically. avg_rating was continuous numerical, while num_of_reviews was discrete numerical, but they were both quantitative features. Both were also transformed using a standard scaler to prevent the different scales from altering coefficients. Ultimately, the model got an F1 score of 0.4655 on the unseen data which is less than ideal. This is likely a result of the model trying to predict an outcome that happens infrequently in the data (around 27% of businesses were 'closed'). I personally believe that this is not a good model because it is limited by linearity and it uses only a few basic features to try and predict a complex outcome which is a business closure.
# Final Model
For my final model I decided to pivot twoards a random forrest classifier. I added the feature 'category'(nominal text), so my final features are 'price', 'avg_rating', 'num_of_reviews', and 'category'. The addition of the 'category' feature was key because different types of restaurants have different clientelle, vloume, risks, overhead, ect. so the category can tell a lot in regards to a restaurants risk of closure. To implement 'category' I had to transform the feature with a count vectorizer which took the list of categories a restaurant was in and made seperate boolean column for each category in 'category'. Another change from the baseline model was transforming num_of_reviews with a quantile transformer instead of a standard scaler. I did this because the data is heavily right skewed due to some longstanding popular restaurants having thousands of reviews and some unpopular or newer restaurants having next to none. Evaluating restaurants number of reviews based on the quantile they're in helps stop outliers from deeply altering the model. I chose the random forrest classifier for my model since I thought my baseline model inaccurately would linearly predict a businesses risk of closure. Random forrest classifier picks up on non linear relationships while resisting outliers and gracefully handling mixed feature types so I thought it was perfect for my model. I did my hyperparameter tuning with GridSearchCV on the training data. I tuned max depth because it controlls the max depth for the decision trees and tuning it will prevent the trees from going overly deep and complex which can lead to overfitting. I also tuned Min samples because tuning the minimum number of samples to split an internal node will prevent the model from overly spliting the data into hyperniche rulesets for very specific restaurants, so ultimately this also prevents overfitting. GridSearchCV found the best hyperparameters to be max_depth of 5 and min_samples_split of 10. After evaluating the model on the unseen data, it scored an F1 score of 0.5397 which is an improvement on the base models F1 score of 0.4655. Some would discredit the models improvements saying the model still has imperfect predictions, however I would argue the model is perfect for its use cases in the real world. In practice someone with a restaurant would have the model predict whether they're closed, if the model says they are then that will highlight the business is at risk and the owner can then take preventive action. The model isint meant to literally find out if a restaurant is closed, it's meant to warn restaurant owners in my focus area in they are projected to close, and it does that well. 
<iframe
  src="assets/FM.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
# Fairness Analysis
For my fairness analysis I will seperate restaurants into two groups, fast food (group X) and non-fast food(group Y). The evaluation metric will be F1 score because the model must be evenly evaluated on its ability to be precise and correctly detirmine 'closed' states
- **Null Hypothesis** - My model is fair. The F1 score for fast food and non-fast food restaurants is roughly the same, any difference comes from random chance
- **Alternate Hypothesis** - My model is unfair. The F1 score for fast food is significantly different from non-fast food. 
- **Test Statistic - Absolute difference between F1 scores
- **Significance** - 0.05
After evaluating, the fast food group got an F1 score of 0.000 and the non-fast food group got an F1 score of 0.5484. This resulted in an abs difference of 0.5484. My permutation test had 1000 repititions where I shuffled the fast food labels to simulate that the fast food label has no effect on the models results. The p-value recieved was 0.07, since thats higher than 0.05 I fail to reject the null. At fist glance the abs difference of 0.5484 implies the model is heavily biased, however since so few restaurants had the fast food category set, shuffling the fast food labels made the fast food group F1 score 0.000 7% of the time. Therefore I fail to reject the null, and cant definitively say my model has significantly different F1 scores in fast food restaurants vs. non-fast food restaurants.
<iframe
  src="assets/FA.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

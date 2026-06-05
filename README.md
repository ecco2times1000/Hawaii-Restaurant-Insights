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
- 

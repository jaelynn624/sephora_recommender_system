# sephora recommender system

![](/Pictures/sephora.jpg)

# Table of Contents 

  * Problem Statement
  * Data Dictionary
  * Executive Summary
  * Findings/Conclusions
  * Recommendations
  * Outside resources

# Problem Statement

The goal of this repository is to create a content based recommender system for various k-beauty products available on "Sephora.com" website. K-beauty has first appeared in 2012 and has reached its peak popularity globally in 2016 and is continuing to grow its market in U.S. For that reason, I have decided to focus on K-beauty products for those who will be interested in seeing what K-beauty products could suit their skincare needs. The website was scraped using selenium. Once all the information has been scraped, and cleaned, it was countvectorized and was used in building a recommender system.  

# Data Dictionary

| Column Name                   | Description                                                   |
|-------------------------------|---------------------------------------------------------------|
| brand_name                    | Name of the brand                                             |
| product_name                  | Name of the product                                           |
| price                         | Price of the product                                          |
| love_num                      | Total number of "loves" the product has                       |
| description                   | Description of the product                                    |
| ratings                       | Rating of the product                                         |
| recommend                     | Percentage of how many customers would recommend this product |
| reviews                       | Number of reviews                                             |
| five_stars                    | Number of 5 stars                                             |
| four_stars                    | Number of 4 stars                                             |
| three_stars                   | Number of 3 stars                                             |
| two_stars                     | Number of 2 stars                                             |
| one_star                      | Number of 1 star                                              |
| vegan                         | If the product is vegan                                       |
| gluten_free                   | If the product is gluten free                                 |
| cruelty_free                  | If the product is cruelty free (no animal testing)            |
| normal_skintype               | Recommended for normal skintype                               |
| dry_skintype                  | Recommended for dry skintype                                  |
| combination_skintype          | Recommended for combination skintype                          |
| oily_skintype                 | Recommended for oily skintype                                 |
| sensitive_skintype            | Recommended for sensitive skintype                            |
| dermatologist_tested          | If the product is dermatologist tested                        |
| without_parabens              | If the product is formulated without parabens                 |
| without_sulfates              | If the product is formulated without sulfates                 |
| without_triclosan             | If the product is formulated without triclosan                |
| without_phthalates            | If the product is formulated without phthalates               |
| without_artificial_fragrance  | If the product is formulated without artificial fragrance     |
| without_triclocarban          | If the product is formulated without triclocarban             |
| without_retinyl_palmitate     | If the product is formulated without retinyl palmitate        |
| without_oxybenzone            | If the product is formulated without oxybenzone               |
| without_mineral_oil           | If the product is formulated without mineral oil              |
| solutions_dryness             | Product helps with dryness of the skin                        |
| solutions_dullness            | Product helps with dullness of the skin                       |
| solutions_oiliness            | Product helps with oiliness of the skin                       |
| solutions_unevenness          | Product helps with uneven skintone                            |
| solutions_pores               | Product helps with minimizing pores                           |
| solutions_elasticity_firmness | Product helps with elasticity and firmness                    |
| solutions_wrinkles            | Product helps with wrinkles (anti-aging)                      |
| solutions_redness             | Product helps with redness of the skin                        |
| solutions_acne                | Product helps fighting acne                                   |
| solutions_puffiness           | Product helps with puffiness                                  |
| solutions_brightening         | Product helps to brighten the skintone                        |
| pt_mask                       | Product type is mask                                          |
| pt_cleanser                   | Product type is cleanser                                      |
| pt_cream                      | Product type is cream                                         |
| pt_serum                      | Product type is serum                                         |
| pt_toner                      | Product type is toner                                         |
| pt_gel                        | Product type is gel                                           |
| pt_moisturizer                | Product type is moisturizer                                   |
| pt_essence                    | Product type is essence                                       |
| pt_mist                       | product type is mist                                          |

# Executive Summary

For this project I scraped Sephora website using selenium. Primarily, selenium is for automating web applications for testing purposes, but is certainly not limited to just that. It allows you to open a browser of your choice & perform tasks as a human being would, such as clicking buttons, entering information in forms, and searching for specific information on the web pages. I have decided to foucs on K-beauty skincare products as it is rapidly gaining popularity since 2012. Sephora has a total of 8 k-beauty skincare brands and is planning to add more in the future. I scraped names of the brands and its products, along with ratings, number of reviews, description, number of stars, number of loves, price, and recommendation percentage (How likely a customer would recommend the product). Next step was EDA and preprocessing. Once I have extracted the information needed, I needed to clean the data. There were some null values which needed to be replaced/dropped, remove punctuations, make everything lower case and change non-categorical columns to floats/integers. 

![](/Pictures/word_count2.png)

I used CountVectorizer to see the most appearing words to extract information out of the description column. I extracted what the product is good for (skincare solution), which skintype it is suitable for, whether the product is vegan, gluten and cruelty free, the type of the product and which chemical the product is formulated without. Once the information was extracted, I have created columns (1 if true 0 if not). 

![](/Pictures/price.png)
![](/Pictures/reviews.png)

The prices of the products were mostly similar except for products from Amore Pacific brand. This brand is in the higher end of the skincare products, which makes sense that it doesn't have as many reviews as the other brands despite the fact that Amore Pacific was the first K-beauty brand to appear on Sephora website (except for innisfree and primera because they were added to the website recently). Not as many people could've easily tried out the product due to its high price compared to other products. 

![](/Pictures/star_ratings.png)
![](/Pictures/ratings.png)

Most of the products had high ratings all above 4 out of 5. More than 65% of the products had 5 stars and less than 5% were either 1 or 2 stars which indicates that customers were pretty satisfied with the products they've purchased. Most of the products were cruelty free (no animal testing) but most products were not vegan. Glow Recipe was the only brand that all of their products were vegan. 

Once EDA and preprocessing was done, I have used sklearn to get cosine similiarities of my dataframe. I have set the product name to be the index since none of the products have the same name(unique). Though it wasn't necessary for my case since my data wasn't too big, I did convert tye type to float16 to optimize the size of a pandas dataframe for low memory environment. 
The final step was evaluation of the recommender system. I have created a function called product recommender where it would return 10 products with highest cosine similarity with the product inputted. product_recommender('Name of the product') will return names of 10 products with highest cosine similarities along with a dataframe of those 10 products sorted by highest ratings. 


# Findings/Conclusions

![](/Pictures/recommender1.png)
Since a recommender system is an unsupervised model, there is no way to measure success other than looking at the value of cosine similarities and personal interpretation. Cosine similarities were pretty decent (all above 0.60). I have noticed, if the product is part of a line with other products (for example, Green Tea products from Innisfree) will have higher cosine similarities. This makes sense because they would be formulated with similar ingredients, will be targeted for similar skin type and skin concerns. 

# Recommendations

For future, I would like to scrape user(customer) ratings and build a user-rating recommender system based on each individual's ratings. Also, I would like to develop a tool where it recommends a specific type of the product. Right now, it is returning all product types based on cosine similarities regardless of what we are looking for. For example, if a Green Tea serum has higher cosine similarity with Green Tea cleanser (which it probability does since they are in the same product line), it will recommend the cleanser when the user is looking for a serum that is similar to Green Tea serum. 

# Outside Sources

https://medium.com/the-andela-way/introduction-to-web-scraping-using-selenium-7ec377a8cf72
https://towardsdatascience.com/web-scraping-using-selenium-836de8677ae5
https://dev.to/lewiskori/beginner-s-guide-to-web-scraping-with-python-s-selenium-3fl9
https://medium.com/@vincentteyssier/optimizing-the-size-of-a-pandas-dataframe-for-low-memory-environment-5f07db3d72e
https://medium.com/free-code-camp/better-web-scraping-in-python-with-selenium-beautiful-soup-and-pandas-d6390592e251
https://medium.com/the-andela-way/introduction-to-web-scraping-using-selenium-7ec377a8cf72
https://www.businessoffashion.com/articles/beauty/korean-beauty-has-hit-the-mainstream-now-what

# Amazon_Vine_Analysis

### Overview of the analysis
The challenge was to analyze Amazon reviews written by members of the paid Amazon Vine program. In Deliverable 1, use PySpark in a Google Colab notebook to perform the ETL process (Extract-Transform-Load) on a specific dataset of product reviews. I chose the Video Games v1 dataset. The transformed dataset is then loaded into an AWS RDS instance (Amazon Web Services Relational Database Service) which is then connected to pgAdmin so that it can be queried with SQL. Then, in Deliverable 2, I used PySpark to determine if favorable reviews are coming more often from Vine members than the general consumers.

#### Results

##### Deliverable 1
Using SparkFiles, the video game dataset is loaded into the Google Colab notebook.

![image](https://user-images.githubusercontent.com/107162310/193130819-af48298a-8b3d-460d-a6de-a5c629309e97.png)

Separate dataframes are created to match the tables that have been created in pgAdmin and which are awaiting the transformed data.

![image](https://user-images.githubusercontent.com/107162310/193130995-4e941f74-dd27-4f58-ba37-b4a69dc85df6.png)

![image](https://user-images.githubusercontent.com/107162310/193131023-a2b5955b-4cc0-4ab9-90d5-9fc0be8fdf60.png)

![image](https://user-images.githubusercontent.com/107162310/193131081-5e9449e8-186d-4893-b335-b94b30b4fd6a.png)

![image](https://user-images.githubusercontent.com/107162310/193131117-964601b5-b845-465b-ab0e-bfe643dae84c.png)

Then the notebook is connected to the AWS RDS instance and the dataframes are loaded.

![image](https://user-images.githubusercontent.com/107162310/193131242-daae8db8-e669-442d-8431-514d9390e4cb.png)

##### Deliverable 2
In a new Google Colab notebook, the Vine dataframe is recreated.

![image](https://user-images.githubusercontent.com/107162310/193131492-94bd77ea-a8aa-4798-a7b7-40659d620f1f.png)

This dataframe is filtered into a new dataframe where the total_votes column is 20+.

![image](https://user-images.githubusercontent.com/107162310/193131769-2d5bf000-6d8a-4d60-8ca9-459ed3bf72a1.png)

Another dataframe is created by filtering the last dataframe to only include rows where the helpful_votes divided by total_votes is 50% or greater.

![image](https://user-images.githubusercontent.com/107162310/193131976-62b74a62-b4a1-4aaf-ade1-93e6a066153a.png)

This dataframe is then filtered twice to separate the Vine reviews into a separate dataframe from the non-Vine reviews.

![image](https://user-images.githubusercontent.com/107162310/193132143-02bcf9f7-1b35-4c74-9485-5fb2586fc723.png)

And then these new dataframes are analyzed to answer the following questions:

  - How many Vine reviews and non-Vine reviews were there?

    ![image](https://user-images.githubusercontent.com/107162310/193132449-8a187eb8-7ecb-4438-86ad-ccce16955fa3.png)

    ![image](https://user-images.githubusercontent.com/107162310/193132590-73333d10-aa89-4810-9217-a10d89218af0.png)

    There were 94 Vine reviews & 40,471 non-Vine reviews.
    
  - How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars?

    ![image](https://user-images.githubusercontent.com/107162310/193132920-56c6b0e6-e595-466e-99b4-902faf5862a8.png)

    ![image](https://user-images.githubusercontent.com/107162310/193132973-9825a250-627e-4ba4-a3f6-b9e242f6de66.png)

    There were 48 Vine reviews that left 5 stars. 15,663 non-Vine reviews that left 5 stars.
    
  - What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars?

    ![image](https://user-images.githubusercontent.com/107162310/193133239-ef049b1c-634d-4722-8ebc-3e51f71a11e8.png)

    ![image](https://user-images.githubusercontent.com/107162310/193133278-3de5f36f-1a46-41a7-9bbb-c50daa20d1cb.png)

    51.06% of Vine reviews were 5 stars. 38.70% of non-Vine reviews were 5 stars.

#### Summary
In the Video Games v1 dataset, initial analysis seems to indicate that there may be a positivity bias for reviews in the Vine program. 51% of Vine members left 5 star reviews, compared to the 38.7% of non-Vine members who left 5 star reviews.

That said, the Vine sample is so much smaller than the non-Vine sample with just 94 reviews compared to 40,471 non-Vine reviews. Therefore, I'm inclined to think we can't be certain that there is a positivity bias with this analysis.

It's possible that non-Vine reviews could be coming from users leaving reviews on products that they may not have actually played. Negative review campaigns have become more prevalent as of late. So, an additional analysis which may help answer the challenge question would be to answer the same questions about non-Vine members, but filter the non-Vine reviews dataset further to include only reviews on verified purchases. This will help eliminate the chance that the percentage of non-Vine 5 star reviews is being held down by disingenuous reviewers.

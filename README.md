# Customer Segmentation with RFM Scores

Hello everyone, in this project I will develop a customer segmentation model using RFM metrics. First we will talk about the RFM and customer segmentation and teach you every single detail about these metrics. After that I will be showing you how to calculate RFM metrics and how can we segment our customers using these metrics in Python. At the end of the project we will take some actions using the RFM Score results.

![r](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/52f407b2-7987-4657-a6e8-9da50e8ed1ee)

Let's get started.

# STEP 1: What is Customer Segmentation and RFM?

### What is customer segmentation and Why do we need it?

Customer segmentation is the process of categorizing a business's customer base into groups based on specific criteria. These criteria typically include demographic characteristics, geographic location, behavioral tendencies, or psychographic factors. Customer segmentation helps businesses optimize their marketing strategies, better address customer needs, and gain a competitive advantage.

The main objective of this process is to understand the different characteristics of different customer groups and to develop sales, advertising and marketing strategies specific to these groups. Each segment may require a customized approach to meet the needs and preferences of a specific target audience.

Customer segmentation also guides the product and service development process. By understanding the needs of different segments, companies can improve their products or develop new products and services. This can increase customer satisfaction and improve overall business performance.

## What is RFM Analysis?

RFM is an analytical method used by companies for customer segmentation and categorizes customers by evaluating them based on Recency, Frequency, and Monetary metrics.

Okey but what is Recency, Frequency and Monetary?

#### RECENCY: This refers to the time since a customer's last purchase. Customers who have made recent purchases are considered more valuable and engaged than those who haven't purchased in a while.

#### FREQUENCY: This measures how often a customer makes purchases. High-frequency customers are those who purchase regularly and are more likely to be loyal to the brand.

#### MONETARY: This represents the total amount of money a customer has spent over a specific period. Customers with high monetary value are those who spend the most and are considered the most valuable to the business.

Yes, we now know the RFM (Recency, Frequency, Monetary) metrics. In next step we will develop a customer segmentation model using the RFM metrics.

# STEP 2: About the Dataset

In this example, we'll use the sales data of a footwear retailer. The dataset includes the shopping history of customers who made their last purchase from a footwear retailer, both online and offline, in 2020-2021.

I'll explain the features we'll be using in the project.

---------------------------------------------------------------------------------------------------------------

master_id: Unique number of customer 

order_channel: The channel used for shopping, indicating the platform (Android, iOS, Desktop, Mobile).

last_order_channel: The channel through which the latest purchase was made.

first_order_date: The date when the customer made their first purchase.

last_order_date: The date of the customer's last purchase.

last_order_date_online: The date of the customer's last online platform purchase.

last_order_date_offline: The date of the customer's last offline platform purchase.

order_num_total_ever_online: The total number of purchases the customer has made online.

order_num_total_ever_offline: The total number of purchases the customer has made offline.

customer_value_total_ever_offline: The total amount spent by the customer in offline purchases.

customer_value_total_ever_online: The total amount spent by the customer in online purchases.

interested_in_categories_12: List of categories in which the customer has made purchases in the last 12 months.

---------------------------------------------------------------------------------------------------------------

Yes, we have enough information about the dataset and features. Now can starting the coding.

# STEP 3: Import the Data and Data Preprocessing, Data Exploration

First of all, we import the necessary libraries and upload the data from our local PC into the Jupyter Lab.

![Screenshot 2023-12-09 154309](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/681e9625-89c2-4be3-9036-2f7f399ee387)

We uploaded the data, let's see the first 5 rows of data.

![Screenshot 2023-12-09 154327](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/83fd4d7b-8cfa-4023-bbe0-1a882b0cc85c)

We have about 20000 different customers and 12 features about those customers as you can see above.

Let's take a look at the featues.

![Screenshot 2023-12-09 155545](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/f6787e48-c1b5-4cc6-a826-3c36bcf2f984)

You already have enough information about the features. Now we should handle the missing values and outliers before calculating the RFM metrics and segmentation. On the other hand, we should convert some columns containing date values to datetime dtype to calculate the RFM metrics.

![Screenshot 2023-12-09 155732](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/38687dcf-40d8-455d-bf42-308c894538a3)

The results:

![Screenshot 2023-12-09 155803](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/5120322f-e408-41b7-be0f-c9a08e9f98f3)

Let's take an overview of the numeric variables.

![Screenshot 2023-12-09 161833](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/64c4514c-fc1c-40cb-ab07-c8041b45230d)

There seem to be outliers. First of all, we should handle the missing and outlier values and then move on to the EDA step. If we want to see outliers here, we can do "EDA" first or use libraries like "Pandas Profiling", but since we only have 4 numeric variables, we can also see outliers with the describe() function, so I did not use visualization tools like boxplot().

Now we write a simple function to see the missing values, this function will return the number of missing values and percentage of missing values for each feature.

![Screenshot 2023-12-09 163702](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/17b9141a-ebdd-466b-9d0e-a25c01ddd6ec)

The results:

![Screenshot 2023-12-09 163711](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/fdd443e6-f5a8-49f9-9efe-92ae91993c7b)

As you can see we have no missing values, this is a good news because each observation is important for us.

Now, we should check the outliers. There are different methods to identify outliers, in this project I will use the IQR method. Let's see these outliers, I have written a simple function to see outliers, in this function we need to write the values Q1 and Q3.

When detecting outliers, I set Q1 and Q3 differently from the usual values of 0.25 and 0.75, which may vary for each data set and the type of analysis you want to perform. I kept the range wider for outliers.

![Screenshot 2023-12-09 164113](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/b554eae0-3db4-41bd-98c6-fd2662d12e67)

The results:

![Screenshot 2023-12-09 164356](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/768dc767-0058-42f6-b184-306a31dde38b)

Now that we have seen our outliers, we can either discard these outliers from the dataset or suppress them according to the values we want, we said that each observation is important, so we will suppress the observations that contain these outliers.

![Screenshot 2023-12-09 165357](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/c6ed0238-4831-4d47-92ce-d79e4485e22d)

The results:

![Screenshot 2023-12-09 165409](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/376c01ce-1eeb-4990-b328-f90c2ecd6fc9)

Now, we have no missing or outlier values. We can move to EDA.

Finally, in this last little step, we will explore the dataset and gain insights about the categorical and numerical variables. To explore the data, we will use the Pandas Profiling library. The "Pandas Profiling" library is a very practical way to perform exploratory data analysis.

Let's explore the data.

![Screenshot 2023-12-09 170935](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/c8cc50fb-18b4-4bf7-a0e4-164cec9c4f4b)

We saved the output as an "HTML" file for easier review and sharing with our teammates if necessary (I will add it to the repo the HTML file)

I will put here some photos from Pandas Profiling for you. For example:

![Screenshot 2023-12-09 171844](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/a09862b8-b84c-4f65-9978-311f7929dc28)
![Screenshot 2023-12-09 171910](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/ce5e2c21-8f50-4f35-a2f5-827154fd3655)
![Screenshot 2023-12-09 171947](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/80670f06-8ca3-4017-bd73-fb166d25f7dd)
![Screenshot 2023-12-09 172000](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/241abd91-ae56-4be5-ad37-3c915893ccee)



Yes, now we can start calculating RFM metrics to perform segmentation.

# STEP 3: Calculating RFM Metrics and Segmentation

Let's copy our dataset to another dataframe and take a look at the first few lines again.

![Screenshot 2023-12-09 175201](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/01c83689-cb4c-4660-9a67-03d4060f32d2)

When doing RFM analysis, we work with historical data, so I set the analysis date as 2 days after the maximum date in the data set.

![Screenshot 2023-12-09 175335](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/9ca2ed6b-449e-4124-874d-0a36ba951990)

Now, we can calculate the RFM metrics. Let's calculate Recency, Frequency and Monetary metrics for each customer.

![Screenshot 2023-12-09 175551](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/0dd1d821-f0fa-44f6-a6c7-270b5ee37422)

Look at the results:

![Screenshot 2023-12-09 175803](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/5db17cf2-ec0d-4576-b93c-8cb66ba39be2)

After calculating the RFM metrics, we need to translate them into RFM scores, which we will record as recency_score, frequency_score and monetary_score.

![Screenshot 2023-12-09 175931](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/8933bc04-f8f3-48d2-9205-a1c28c4aae10)

The results:

![Screenshot 2023-12-09 180002](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/3c3b04ea-4f8f-46d4-a952-e163e4a179cd)

Let's create two variables named RF_SCORE and RFM_SCORE with the metrics we calculated and assign the RFM scores of each customer to these variables.

![Screenshot 2023-12-09 180408](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/68c44c16-3dd8-4f83-b72f-69ede346be4d)

Let's see the RF and RFM scores for each customer.

![Screenshot 2023-12-09 180910](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/f89d5cbf-8dab-4b33-bfaf-17aa3f4f7694)

We need to define segments for the RF scores created.

![Screenshot 2023-12-09 180939](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/f1b30336-6a08-4cb5-ad9a-ba4f4081cfcb)

The segmentation results:

![Screenshot 2023-12-09 181138](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/d9cb96ce-cefb-46c8-a05b-dc8abf3367b7)

Let's see how many customers we have in which segment.

![Screenshot 2023-12-09 181355](https://github.com/enesbesinci/CRM-customer-segmentation-using-RFM/assets/110482608/a80bfd27-e27e-42a7-ad46-ea147bd3224c)

Let's use the describe() function to examine the statistical summary of each segment and save this table in a csv file.

Yes, we have now analyzed each of our customers with RFM metrics and created customer segments. After this stage, we should engage in sales, advertising and marketing activities specific to each customer segment.

# STEP 4: Marketing Scenario

In this step we w

























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





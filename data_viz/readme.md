## Data visualization with Amazon S3 and Amazon QuickSight

### Unicorn Companies

### 1) Dataset

Private companies with a valuation over $1 billion as of March 2022, including each company's current valuation, funding, country of origin, industry, select investors, and the years they were founded and became unicorns.

Source: https://www.kaggle.com/datasets/deepcontractor/unicorn-companies-dataset


### 2) Step by Step

- Save data set from Kaggle related to Unicorn Companies in 2022
  
- Create a S3 bucket where you will include the data files
  
- Upload the both the csv file and also the manifest.json into the bucket (don't forget to edit the manifest.json file with the name of your bucket)
  
- Carry out a brief SQL data check query with the S3 SELECT function
  
<img width="1509" alt="Screenshot 2023-10-06 at 14 42 35" src="https://github.com/jgalvalisi/AWS/assets/97465207/d9cbb2f0-29c9-4634-90f8-158fef32df2d">

<img width="1501" alt="Screenshot 2023-10-06 at 13 59 47" src="https://github.com/jgalvalisi/AWS/assets/97465207/04ce59d7-ded3-4542-acf0-784592fed03f">

- Go to Amazon QuickSight and connect it to your bucket with the manifest.json file copying the S3 URl
  
- Create data visualizations in Amazon QuickSight

<img width="723" alt="Screenshot 2023-10-06 at 14 21 56" src="https://github.com/jgalvalisi/AWS/assets/97465207/7a59a230-208d-43dc-8b27-cdb04e7f59e0">

<img width="791" alt="Screenshot 2023-10-06 at 13 22 45" src="https://github.com/jgalvalisi/AWS/assets/97465207/1ebc31f0-cd30-4505-9a3b-8b00c2a4e376">

<img width="781" alt="Screenshot 2023-10-06 at 14 24 27" src="https://github.com/jgalvalisi/AWS/assets/97465207/9f383bbb-4f55-48b8-9823-83fa5db84ab3">

<img width="470" alt="Screenshot 2023-10-06 at 13 35 45" src="https://github.com/jgalvalisi/AWS/assets/97465207/e62e7414-5e55-4ac7-84a9-0b786f467154">

- Analysis
  
  - The three best-valued unicorns in the world have a valuation above $100B and come from China (Bytedance and SHEN) and the United States (SpaceX)
  - New York is the city with the most unicorns in the world with 152
  - Within South America, Brazil is the country with the most unicorns with 21 (76%)





# Home Sales

For this project, home sales data was read into a Spark DataFrame from an AWS S3 bucket:

![Screenshot 2023-09-25 at 17 46 44](https://github.com/ashejaz/Home_Sales/assets/127614970/2ecb96d6-f416-44c2-b2e2-c9c43f1b0272)

A temporary view for the table was created and the table was then queried using SparkSQL.

The aim of this project was to compare the run-times of the following query on the regular data vs cached data vs partioned parquet data:

>_What is the "view" rating (to 2 decimal places) for homes costing more than or equal to $350,000?_

The query performed on the initial home sales table returned the following output and run-time:

![Screenshot 2023-09-25 at 17 33 20](https://github.com/ashejaz/Home_Sales/assets/127614970/245a59f7-273c-476d-a7d6-9acc11b5e302)

Then, the home sales table was cached and the query was performed again, returning the following result:

![Screenshot 2023-09-25 at 17 33 31](https://github.com/ashejaz/Home_Sales/assets/127614970/1c846b58-74b6-49c5-b822-3d9e27685eb1)

Finally, the data was partitioned on the 'date_built' column and formatted to parquet. The query was run a final time to return the following:

![Screenshot 2023-09-25 at 17 33 42](https://github.com/ashejaz/Home_Sales/assets/127614970/5002cd03-22e1-4705-a80d-e76265b15732)


To conclude, we can see from the run-times that caching the table sped up the query as expected. However, when the data is partitioned and formatted to parquet, the query executes slower than it did in the 2 previous instances. This may be because this dataset is small and partitioning & parquet work best on large datasets. In this instance, partitioning may be using more resources thus slowing down the query. For this dataset, the best way to optimise query run-time would therefore be simply caching the table.

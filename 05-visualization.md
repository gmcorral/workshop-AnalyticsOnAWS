## Data visualization

So far, we have imported a raw dataset into our central data lake on Amazon S3, created a data catalog automatically with AWS Glue, performed data discovery using standard SQL queries with Amazon Athena and queried data from our DW cluster. 

The last step to complete our analytics on AWS journey is to visualize the data in a way that can be easily consumed by the business. For that we are going to make use of [Amazon QuickSight](https://quicksight.aws/) a fast, cloud-powered business intelligence service that makes it easy to build visualizations, perform ad-hoc analysis, and quickly get business insights from your data.

1. Navigate to the [Amazon QuickSight console](https://quicksight.aws.amazon.com/). If this is the first time you access QuickSight, click *Sign up for QuickSight*. Choose the *Standard* edition and click **Continue**

2. On the *Create your QuickSight account* specify:
	* a globally unique name for your quicksight account
	* an email address for notifications
	* the region that you have been using throught the workshop: US East (N. Virginia)

1. Scroll down the page and make sure that your QuickSight account has access to S3 by selecting **Amazon S3**.

	![QuickSight enable S3](images/21a-quicksight-select-s3.png)

1. Click on the **Choose S3 bucket** link and select your data bucket `<workshop-bucket>`. 

	![QuickSight enable data bucket](images/21b-quicksight-select-buckets.png)

	Click **Select buckets** and proceed to provision your QuickSight account.
	
1. Once your QuickSight account is provisioned you can always refine/change access to resources by clicking the <img src=images/21d-quicksight-manage-icon.png width=12px> icon and **Manage QuickSight**

	![QuickSight manage](images/21c-quicksight-manage.png)

1. Go back to the [Amazon QuickSight home](https://quicksight.aws.amazon.com/) and click **Manage data**. Click **New data set** to create a data set. Select **Athena**

	![QuickSight new data set](images/23-quicksight-new-dataset.png)
	
1. Specify a name for the data set, for example, `nyc-tlc-dataset` and click **Create data source**

	![QuickSight create data set](images/24-quicksight-create-dataset.png)

	Select `nyc-tlc` as database and `yellow`as table. Click **Select**

	![QuickSight create data set](images/25-quicksight-dataset-tables.png)
	
	Select **Directly query your data** and click **Edit/Preview data**

	![QuickSight create data set](images/25b-quicksight-dataset-spice.png)
	

2. Change the data source name to `nyc-tlc-tripdata`. 

	![QuickSight create data set](images/26a-quicksight-dataset-edition.png)

1. Add a calculated field by selecting **Fields** and clicking **Add calculates field**. We want a field called `hour_of_day` that we will compute extracting the hour from the `tpep_pickup_datetime` source field. Leverage Amazon QuickSight built-in functions for that: `extract('HH', parseDate({tpep_pickup_datetime}, 'yyyy-MM-dd HH:mm:ss'))`

	![QuickSight create data set](images/26b-quicksight-dataset-edition.png)
	
	Click **Create**

2. Add another calculated field by selecting **Fields** and clicking **Add calculates field**. We want a field called `pickup_daytime` that we will compute extracting the time into a date field from the `tpep_pickup_datetime` source field. Leverage Amazon QuickSight built-in functions for that: `parseDate({tpep_pickup_datetime}, 'yyyy-MM-dd HH:mm:ss'))`

	![QuickSight create data set](images/26c-quicksight-dataset-edition.png)
	
	Click **Create**

3. Create now a visualization by clicking **Save & Visualize**. From **Visual types** choose a line chart <img src=images/27-quicksight-line-chart-icon.png width=10px>. From the **Fields list** drag **pickup_datetime** and drop it into the **X axis** box. By default timestamp data types are aggregated by day, but you can adjust it to your preference. From the **Fields list** drag **vendorid**, which identifies the taxi company, and drop it into the **Color** box.

	![QuickSight line chart](images/28a-quicksight-line-chart.png)
	
	If you see something like the above is because your dataset contains a few outlier records with dates outside the range. Use a filter to get a better visualization. Click on the <img src=images/28b-quicksight-filter-icon.png width=12px> icon and create a filter for the `pickup_daytime` field, with the following settings:
	
	* *All visuals*
	* Filter type: *Time range*, *Between*
	* Start date: `2017-11-01 00:00`
	* End date: `2017-12-31 23:59`

	Click **Apply**
	

	![QuickSight line chart](images/28c-quicksight-line-chart-filtered.png)
	
	Explore the different options you have to customize the chart.

4. Add a second chart by clicking **Add**, **Add visual**

	![QuickSight line chart](images/29-quicksight-add-visual.png)

2. Add a heat map chart <img src=images/30-quicksight-heat-map-icon.png width=10px>. From the **Fields list** drag **pickup_datetime** and drop it into the **Rows** box. Drop the calculated field **hour\_of\_day** into the **Columns** box.

	![QuickSight line chart](images/31-quicksight-heat-map.png)
	
	Notice the different pattern beetween work days and weekends and how easily you can tell them appart using the heat map chart.	
	
	
### Congratulations! You completed the data visualization part

[Back to home page](README.md)

[Back to top](#data-visualization)



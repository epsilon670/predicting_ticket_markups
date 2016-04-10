<h1>Analyzing Concert Data to Predict Ticket Price Markups</h1>

Author: Evan Paul
https://www.linkedin.com/in/evan-paul-b4b94a55 

GitHub link: https://github.com/epsilon670/predicting_ticket_markups 

Presentation Slides URL: http://res.cloudinary.com/general-assembly-profiles/image/upload/v1460329211/bmgg4spyiq520hhq1hki.pdf

<h3>Overview</h3>
This was my final project for General Assembly’s part time Data Science class given in San Francisco from January-April 2016 (https://generalassemb.ly/education/data-science).

The goal was to build a model that could predict the ticket markup of a concert on StubHub.com (an online ticket re-selling marketplace) given inputs about the concert. If these values could be predicted, a ticket re-seller could use the prediction to estimate an ideal selling price when posting their tickets on StubHub. Similarly, a concertgoer could use the predictions to estimate how much they would need to pay in order to buy tickets for a given show from StubHub.

A slideshow deck outlining this project, its scope, and my key findings can be viewed in the <b>Analyzing Concert Data to Predict Ticket Price Markups.pdf</b> file.

<h3>Data Collection</h3>
I collected the data for this project from 3 primary sources:

StubHub’s Web API (to get StubHub ticket price data for concerts)<br>
Web scrapes of SongKick.com (to get ticket face values and “sold out” statuses for concerts)<br>
EchoNest Web API (to get data relating to concert artists’ popularities)<br>

I collected this data for concerts in 16 metropolitan areas across the United States. To ensure consistency between concerts, I collected all data on March 13th, 2016. The code for collecting all data for each metro area can be viewed in the <b>Initial_Data_collection.ipynb</b> notebook and the code for aggregating all of the metro area concert data together can be viewed in the <b>Create_master_dataframe.ipynb</b> Jupyter notebook.

In total, I collected data for 3,126 concerts. This raw, unprocessed data can be found in the <b>Data/MasterTicketData.csv</b> file.

<h3>Data Processing and Cleaning</h3>
Once the data was collected, I ran Python code to process the data and clean it. This included:

Removing concerts with non-numeric ticket prices<br>
Calculating ticket markup by subtracting face value from StubHub’s minimum ticket price<br>
Removing outliers (using the IQR method)<br>
Converting variables with large skews to logarithmic form<br>

The code for the processing and cleaning can be found in the <b>Process TicketData.ipynb notebook</b>. The code for converting feature values into logarithmic form can be viewed in the <b>Examine Variable Distributions & Skews.ipynb</b> notebook.

The final processed data set of 1,192 concerts is in the <b>Data/ProcessedTicketDataLogs.csv</b> file.

Noteworthy problem with data - the web scrapes of SongKick did not always yield the correct “sold out” values. Only 80 out of 1,192 concerts are listed as “sold out” in the data. I’ve confirmed that at least 1 show (and likely many more) marked as “not sold out” in the dataset was actually sold out in reality. Therefore, it is highly likely that the dataset underrepresents the true number of sold out shows (meaning that the impact of a show being sold out is underestimated in the resulting models).

<h3>Regression Model</h3>

Once a clean and processed dataset was created, I then used the RandomForestRegressor package from sklearn.ensemble to build a Random Forest model for ticket markup prediction. The code for this can be viewed in the <b>Ticket Markup Prediction Model.ipynb</b> notebook.

<h3>Classification Model</h3>

In order to try and get more accuracy in the predictions, I then tried to build a classification model to predict the dollar range that a concert ticket’s markup would be in. This followed the same process as in regression, except I used RandomForestClassifier from sklearn.ensemble in order  to classify each concert into one of the following buckets:

Bucket 1: Ticket markup between $0 - $25 <br>
Bucket 2: $25 - $37 <br>
Bucket 3: $37-$52 <br>
Bucket 4: >$52 <br>

The code for the classification model can be viewed in the <b>Ticket Markup Classification Model.ipynb</b> notebook.

<h3>Linear Regression</h3>

I also used Lasso and Linear Regression on the data in order to see whether there were any interesting insights that could be gleaned from the dataset. The code for this can be found in the <b>Linear Regression for Stubhub Markup.ipynb</b> notebook. See the <b>Analyzing Concert Data to Predict Ticket Price Markups.pdf</b> file for the results.

<h3>Libraries and 3rd Party Packages</h3>

I used the following libraries in this project:

Pandas<br>
sklearn<br>
NumPy<br>
Matplotlib<br>
statsmodels.formula.api<br>
Beautiful Soup (for web scraping)<br>

Suggestions, feedback, comments, and pull requests are all welcome.


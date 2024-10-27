## <a href="https://app.powerbi.com/home" target="_blank"> <img src="https://www.ptr.co.uk/sites/default/files/powerbilogo.png" alt="powerbi" width="40" height="40"/> </a> Power BI projects 

Hello!
Here you can find a detailed Power BI projects tasks.

<details><summary><h3> <a href="https://app.powerbi.com/home" target="_blank"> <img src="https://www.ptr.co.uk/sites/default/files/powerbilogo.png" alt="powerbi" width="25" height="25"/> </a>📈Power BI bussines sales analysis </h3></summary>

  Task: choose 2 teams and present the data analysis insights.
  Teams: Executive Leadership and Sales.

1. Provide 1 dashboard which you will then use for 2 presentations for each of the departments.
2. You should add at least 1 new data source to the dashboard.
3. Write [SQL queries](https://github.com/Ingrik07/Ingrida_intro/blob/main/SQL/SQL_sales_analysis.md) to extract needed data, these queries should be well documented. <img src="https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExOTVzZnkxeWk3bnZkZm1lN25pa2o0ZHBmNzB4emdiaXEwcmswcDR6MSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/JIX9t2j0ZTN9S/giphy.gif" width="5%" height="5%" />
4. Work on the clean and clear dashboard structure. Have clear labels, good naming conventions and other elements, so the audience who looks at your dashboard can understand it without your explanations.
5. Insights on Power BI sales analysis.
> **Major Increase in ONLINE orders due to price strategy change.**
<p align="center">
  <img src="https://github.com/Ingrik07/Ingrida_intro/blob/main/Logos/Screenshots/image1.png"></img>
</p>

> **The main reason starting from 2003 July became 'price'.**

<p align="center">
  <img src="https://github.com/Ingrik07/Ingrida_intro/blob/main/Logos/Screenshots/image2.png" alt="sales reason price" width="70%" height="70%"></img>
</p>

> **Since Online sales increased due due to low price policy, the offline AOV remained to be x10 times higher than online AOV.**

<p align="center">
  <img src="https://github.com/Ingrik07/Ingrida_intro/blob/main/Logos/Screenshots/aov%20capture.JPG" alt="sales reason price" width="70%" height="70%">
</p>
</ br>

> **Added sales map representing the country markets by sales and products.**
</details>
</details>

<details><summary><h3> <a href="https://app.powerbi.com/home" target="_blank"> <img src="https://www.ptr.co.uk/sites/default/files/powerbilogo.png" alt="powerbi" width="25" height="25"/> </a>Power BI RFM analysis </h3></summary>

1. Use SQL for calculation and data selection. ([HERE](https://github.com/Ingrik07/Ingrida_intro/blob/main/SQL/rfm_sql_analysis.md) you can find the SQL code <img src="https://c.tenor.com/bCfpwMjfAi0AAAAC/cat-typing.gif" width="5%" height="5%" />)
2. Present your RFM analyses with a dashboard by using Power BI.
3. Insights on RFM analysis.

<p align="center">
  <img src="https://github.com/Ingrik07/Ingrida_intro/blob/main/Logos/Screenshots/RFM%20bubbles.JPG" width="70%" height="70%">
</p>

> The most profitable customers segment - **Best Customers**. They have highest frequency and monetary scores. Although the customers are quite active (purchases are recent), they should be awarded for loyalty with exceptional deals dedicated to them.
> **Big spenders** - the 2nd highest monetary rate, but their purchases are average recency. We should provide them with more targeted/personalized offers.
> 
> **Can't lose them** - although the customers have lower than average monetary base and average frequency, they still add up to the business revenue, these should receive some exceptional attention: combined personalized deals, inclusion into loyalty program, awards for purchases.
> 
> **Recent customers** - loyalty program should be provided to them. Their purchase should followed up with asking for the feedback, providing loyalty program and keeping them informed about the best deals.

<p align="center">
  <img src="https://github.com/Ingrik07/Ingrida_intro/blob/main/Logos/Screenshots/segments.JPG" width="70%" height="70%">
</p>

> The most profitable customers segment - **Best Customers**. They have highest frequency and monetary scores. Although the customers are quite active (purchases are recent), they should be awarded for loyalty with exceptional deals dedicated to them.
> **The lost customers** segment takes almost the same part from total customers number as the best customers.
> The good sign here is that we have the widest best customers segment (considering that we took best scores).
>
> **Recent customers** - the ones who have purchased recently but have no loyalty, are first-timers, etc. These take also pretty considerable part of all customer base and they require a lot of attention.
>
> **11% require especially urgent and clear attention**, since their purchase was quite a while ago (3/4 quartiles) but they have at least average monetary score.
> **Loyal customers** base is quite small, so this shows that we need to grow regular buyers base (even if it's average spending).

</details>

<details><summary><h3> <a href="https://app.powerbi.com/home" target="_blank"> <img src="https://www.ptr.co.uk/sites/default/files/powerbilogo.png" alt="powerbi" width="25" height="25"/> </a>Website sessions data analysis </h3></summary>

### Sprint: Marketing Analytics

Dataset: _raw_events_

The goal of the analysis is to explore turing_college.raw_events dataset and find useful insights about the customer behaviour on the website.
The analysis answers to he main questions as:
1) identify if users tend to spend more time on the certain weekdays,
2) to analyse how audience tend to act on different weekdays and campaigns;
3) Customers behaviour by country.
4) find the other useful insights.


## Main takeaways:
- Most of the sessions have no campaigns assigned (99.5%).
- ‘Data share promo’ has the highest number of assigned sessions (1656). It means that there were one big or many campaigns in collaboration with the partners (or booked campaigns).
- The biggest portions (16.6-16.8%) of total sessions Wednesdays and Thursdays (no matter the month).
- The biggest portions (6.09%-7.09%) of total sessions Wed-Thu-Fri in December. In November, people are most active on Tuesday.
- Longest durations appear on BF V2 campaign Monday/Tuesday/Saturday and NY V2 campaign Sunday.
- Sessions are registered from 109 countries. 3 of them represent ~60% of audience.

Report slides: [HERE](https://docs.google.com/presentation/d/1Ckrv7hqwxQz57Cllne9TiZ8wo3a6585J3stop27x8ZY/edit?usp=sharing)
SQL code:
[Here](https://console.cloud.google.com/bigquery?sq=147855269776:80e7942712334bf3ad6725daaa0f5234) you can find the code.

Power BI full dashboard:
[HERE](https://github.com/Ingrik07/Ingrida_intro/blob/main/PowerBI/sessions_data.pbix)

</details>


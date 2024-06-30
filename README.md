## Hello, I am Ingrida!

<picture>
 <source media="(prefers-color-scheme: dark)" srcset="https://github.com/Ingrik07/Ingrida_intro/blob/main/Screenshot%202024-06-28%20at%2015.39.05.png">
 <source media="(prefers-color-scheme: light)" srcset="https://github.com/Ingrik07/Ingrida_intro/blob/main/Screenshot%202024-06-28%20at%2015.39.05.png">
 <img alt="See-my-image" src="https://github.com/Ingrik07/Ingrida_intro/blob/main/Screenshot%202024-06-28%20at%2015.39.05.png">
</picture>


<h2 align="left">👨🏻‍💻 About Me:</h2>
 
- 💻 Currently I am influencers marketing senior specialist
- 👩‍🎓 Finished CodeAcademy Big Data courses
- 👩🏻‍💻📓💻 Currently studying at Turing College Data analytics courses
- ⚡ Fun fact: I also hold MA degree in Political science/European studies field
- 
<h3> ✉️Contact me </h3> 
<p align="left">
    <a href="https://www.linkedin.com/in/ingrida-ivinskait%C4%97-08b5837b/" target="_blank"> <img src="https://pngimg.com/uploads/linkedIn/linkedIn_PNG31.png" alt="html5" width="105" height="40"/a> <a href="mailto:ingrik0713@gmail.com"> <img align="left" alt="Gmail" width="130" hight="100" src="https://github.com/Xx-Ashutosh-xX/Xx-Ashutosh-xX/blob/master/assets/icons/gmail.png" width="100" height="40"/>
     </p>

## Table of Contents

- [My skills](#My_skills)
- [Power_BI](#Power_BI)
- [SQL examples](#SQL)
- [CLV](#CLV)
- [A/B_testing](#[A/B_testing)
- [Funnels](#Funneks)
- [Acknowledgments](#acknowledgments)


## My Skills
<details>
<summary>💻 My top coding languages</summary>

<h2 align="left">:hammer_and_wrench: Technologies and Tools I use:</h2>
<p align="left">
    <a href="https://console.cloud.google.com/bigquery" target="_blank"> <img src="https://w7.pngwing.com/pngs/182/372/png-transparent-google-bigquery-hd-logo.png" alt="css3" width="40" height="40"/> </a>
<a href="https://sass-lang.com" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/sass/sass-original.svg" alt="sass" width="40" height="40"/> </a>
    <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="40" height="40"/> </a>
<a href="https://webpack.js.org/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/js_webpack/js_webpack-icon.svg" alt="webpack" width="40" height="40"/> </a>
<a href="https://reactjs.org/" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original-wordmark.svg" alt="react" width="40" height="40"/> </a>
<a href="https://www.gatsbyjs.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/gatsbyjs/gatsbyjs-icon.svg" alt="gatsby" width="40" height="40"/> </a>
      <a href="https://nodejs.org" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nodejs/nodejs-original-wordmark.svg" alt="nodejs" width="40" height="40"/> </a>
    <a href="https://expressjs.com" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/express/express-original-wordmark.svg" alt="express" width="40" height="40"/> </a>
    <a href="https://www.mongodb.com/" target="_blank"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" alt="mongodb" width="40" height="40"/> </a>
<a href="https://www.postman.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg" alt="postman" width="40" height="40"/> </a>
<a href="https://git-scm.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a>
<a href="https://azure.microsoft.com/en-us/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/microsoft_azure/microsoft_azure-icon.svg" alt="azure" width="40" height="40"/> </a>
 <a href="https://cloud.google.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/google_cloud/google_cloud-icon.svg" alt="google cloud" width="40" height="40"/> </a>
 <a href="https://firebase.google.com/" target="_blank"> <img src="https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg" alt="firebase" width="40" height="40"/> </a>
    </p>
</details>
 
 <details>
<summary>🤓 My analytical and field skills</summary>

|  | Skills |
|-----:|---------------|
|     1|Finding and presenting OKRs |
|     2|Answering advanced marketing questions |
|     3|A/B testing |
|     4|Helping to improve business performance |
</details>

## Power BI
-- Power BI Screenshots and files

## SQL

<details>
<summary><a href="https://console.cloud.google.com/bigquery?sq=147855269776:a9a7016a5d384587b29dedab17b22b67" target="_blank"> <img src="https://w7.pngwing.com/pngs/182/372/png-transparent-google-bigquery-hd-logo.png" alt="css3" width="20" height="20"/> </a>  Big Query Customer life time value calculation example</summary>

```
WITH
  cohort_weeks AS ( --defining the cohort weeks
  SELECT
    user_pseudo_id AS user_id,
    MIN(DATE_TRUNC(PARSE_DATE('%Y%m%d', CAST(event_date AS String)), WEEK)) AS cohort_week
  FROM
    `tc-da-1.turing_data_analytics.raw_events`
  GROUP BY
    user_pseudo_id),

  sum_rev AS ( --defining the revenue
  SELECT
    user_pseudo_id AS user_id,
    purchase_revenue_in_usd AS revenue,
    DATE_TRUNC(PARSE_DATE('%Y%m%d', event_date), WEEK) AS purchase_week
  FROM
    `tc-da-1.turing_data_analytics.raw_events` )

SELECT 
  w.cohort_week,
  ROUND(SUM(
      CASE
        WHEN purchase_week = cohort_week THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_0,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 1 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_1,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 2 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_2,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 3 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_3,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 4 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_4,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 5 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_5,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 6 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_6,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 7 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_7,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 8 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_8,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 9 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_9,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 10 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_10,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 11 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_11,
  ROUND(SUM(
      CASE
        WHEN purchase_week = DATE_ADD(cohort_week, INTERVAL 12 week) THEN revenue
    END
      ) / COUNT(DISTINCT w.user_id), 4) AS week_12
FROM
  cohort_weeks AS w
LEFT JOIN
  sum_rev r
ON
  w.user_id = r.user_id
GROUP BY
  w.cohort_week
ORDER BY
  w.cohort_week
```
</details>

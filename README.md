# MetroCar

## Project Overview

In this project, I delved into Metrocar's customer funnel, similar to renowned ride-sharing platforms like Uber and Lyft. Utilizing SQL for data analysis and Tableau for visualization, I unearthed crucial insights to refine Metrocar's user experience and increase conversion rates. Guided by stakeholders' inquiries, I identified key areas for optimization within the customer journey. My task was to conduct a thorough funnel analysis, presenting actionable recommendations supported by data-driven insights.

## Data Source

MetroCar Dataset: This dataset is inspired by publicly available datasets for Uber/Lyft. The data for this dataset was generated specifically for this project.
[Masterschool-Project](https://www.postgres://Test:bQNxVzJL4g6u@ep-noisy-flower-846766-pooler.us-east-2.aws.neon.tech/Metrocar)  

## Business Questions

- What steps of the funnel should we research and improve? Are there any specific drop-off points preventing users from completing their first ride?
- Metrocar currently supports 3 different platforms: ios, android, and web. To recommend where to focus our marketing budget for the upcoming year, what insights can we make based on the platform?
- What age groups perform best at each stage of our funnel? Which age group(s) likely contain our target customers?
- Surge pricing is the practice of increasing the price of goods or services when there is the greatest demand for them. If we want to adopt a price-surging strategy, what does the distribution of ride requests look like throughout the day?
- What part of our funnel has the lowest conversion rate? What can we do to improve this part of the funnel?

### Query Sample

- Metrocar currently supports 3 different platforms: ios, android, and web. To recommend where to focus our marketing budget for the upcoming year, what insights can we make based on the platform?

```
SELECT 
    platform,
    COUNT(DISTINCT a.app_download_key) AS app_downloads,
    COUNT(DISTINCT s.user_id) AS signups,
    COUNT(DISTINCT r.ride_id) AS ride_requests,
    COUNT(DISTINCT CASE WHEN r.dropoff_ts IS NOT NULL THEN r.ride_id END) AS completed_rides,
    ROUND(SUM(t.purchase_amount_usd)::numeric, 2) AS total_revenue
FROM
    app_downloads AS a
JOIN
    signups AS s ON a.app_download_key = s.session_id
JOIN
    ride_requests AS r ON s.user_id = r.user_id
LEFT JOIN
    transactions AS t ON r.ride_id = t.ride_id
GROUP BY
    platform
ORDER BY
    platform;
```

## Tableau Visualizations

### Performance Analysis  in Funnel (Percent From First vs. Percent From Previous)

Funnel visualization is ideal for this analysis because it provides a clear visual representation of the customer journey through distinct stages, allowing for easy identification of conversion rates and drop-off points. By juxtaposing "Percent of Top" and "Percent of Previous" metrics, it offers valuable insights into user behavior and engagement patterns at each stage of the funnel. This visualization format enables stakeholders to quickly grasp the effectiveness of their marketing and conversion strategies, pinpoint areas for improvement, and make data-driven decisions to optimize the customer journey and drive business growth.
![1](https://github.com/Sanjeev-Lama/MetroCar/assets/158605914/4da94514-93a4-49d5-9454-a2e1dc8f38d1) 

### Platform Based Analysis Across Different Age Range

offers a concise way to assess user engagement and conversion rates across different platforms and age groups. By employing the percent of top and percent of previous metrics on the left and right sides, respectively, stakeholders can easily discern trends and performance variations. This format facilitates quick comparisons between platforms and age segments, enabling targeted interventions and strategic adjustments to maximize user acquisition and retention efforts.



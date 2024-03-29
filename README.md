# MetroCar

## Table of Content

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Business Questions](#business-questions)
  - [Query Sample](#query-sample)
- [Tableau Visualizations](#tableau-visualizations)
  - [Performance Analysis In Funnel](#performance-analysis-in-funnel)
  - [Platform Based Analysis Across Different Age Range](#platform-based-analysis-across-different-age-range)
  - [Age Group Performance](#age-group-performance)
  - [Ride Trends On Platforms Over Time](#ride-trends-on-platforms-over-time)
- [Recommendations](#recommendations)
- [Links](#links)

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

### Performance Analysis In Funnel

Funnel visualization is ideal for this analysis because it provides a clear visual representation of the customer journey through distinct stages, allowing for easy identification of conversion rates and drop-off points. By juxtaposing "Percent of Top" and "Percent of Previous" metrics, it offers valuable insights into user behavior and engagement patterns at each stage of the funnel. This visualization format enables stakeholders to quickly grasp the effectiveness of their marketing and conversion strategies, pinpoint areas for improvement, and make data-driven decisions to optimize the customer journey and drive business growth.
![1](https://github.com/Sanjeev-Lama/MetroCar/assets/158605914/4da94514-93a4-49d5-9454-a2e1dc8f38d1) 

### Platform Based Analysis Across Different Age Range

This visualization offers a concise way to assess user engagement and conversion rates across different platforms and age groups. By employing the percent of top and percent of previous metrics on the left and right sides, respectively, stakeholders can easily discern trends and performance variations. This format facilitates quick comparisons between platforms and age segments, enabling targeted interventions and strategic adjustments to maximize user acquisition and retention efforts.
![2](https://github.com/Sanjeev-Lama/MetroCar/assets/158605914/a03b4a3b-a8f8-4b35-a12a-7636093bc1d8)

### Age Group Performance 

Using a line chart for this visualization allows for a detailed examination of user engagement at each stage of the funnel across different age groups. By segmenting the data by age range and funnel step, stakeholders can identify performance trends and potential bottlenecks. The color-coded lines represent each funnel step, offering a clear visual representation of user progression. Leveraging the tooltip to display the percentage of the current value relative to the first value enhances interpretability, enabling stakeholders to assess relative performance effectively.
![3](https://github.com/Sanjeev-Lama/MetroCar/assets/158605914/69316896-97a9-4381-a8a8-b0a490888aef)

### Ride Trends On Platforms Over Time 


Utilizing a line graph provides a comprehensive view of ride activity across different platforms over time. The graph's x-axis represents months, offering a temporal perspective, while the y-axis shows the total ride count. Segmenting the data by platform enables stakeholders to discern usage patterns specific to each platform. The color-coded lines distinguish between platforms, aiding in comparative analysis. Leveraging the label to display the total ride count enhances data interpretation, facilitating trend identification and performance evaluation.
![4](https://github.com/Sanjeev-Lama/MetroCar/assets/158605914/c9bd376a-4ec3-4943-857a-de417562ebe1)

## Recommendations

1. **Simplify Onboarding:** Simplify the app download and signup process to reduce friction and increase conversion rates. Consider offering personalized incentives to encourage more downloads to convert into signups seamlessly.

2. **Optimize Ride Requests:** Streamline the ride request process to minimize drop-offs and improve user satisfaction. Enhance features such as real-time updates and smoother navigation to ensure a seamless experience for users.

3. **Encourage Payment Completion:** Incentivize users to complete payments promptly after rides to boost revenue and enhance user engagement. Implement discounts or loyalty rewards to encourage timely transactions and foster positive user experiences.

4. **Prompt User Reviews:** Prompt users to leave reviews post-ride by leveraging strategic prompts or incentives within the app. Positive reviews not only enhance brand reputation but also provide valuable feedback for service improvements.

5. **Targeted Marketing Strategies:** Develop platform-specific marketing strategies based on performance data to optimize resource allocation. Tailor campaigns to resonate with the demographics and preferences of users across different platforms for maximum impact.

## Links

1. Help from [ChatGPT](https://chat.openai.com/share/053889bb-509a-4d8b-b6bd-af7f625e1eec)
2. My Approach and Queries are [here](https://docs.google.com/document/d/1DpV52-KWK0GyTt8HloUf6Ge9Rv0JVoNFHcyPmhvqiBE/edit)
3. Tableau Story Visualization [here](https://public.tableau.com/app/profile/sanjeev.lama/viz/ProjectMetroCar/MetroCarAnalysis?publish=yes)
4. [Video Analysis](https://screenapp.io/app/#/shared/70dbb59c-182d-48c3-b010-7995ad47fdec)
5. Project Presentation [here](https://github.com/Sanjeev-Lama/MetroCar/files/14319387/MetroCar.Project.1.pdf) 

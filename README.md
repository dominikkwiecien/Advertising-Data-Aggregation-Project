
# Advertising Data Aggregation Project

## Project Overview

This project demonstrates the process of combining and analyzing advertising data from multiple sources using SQL. The goal is to aggregate key performance metrics for advertising campaigns run on Google Ads and Facebook Ads. By leveraging **Common Table Expressions (CTE)** and the **UNION ALL** operator, the project consolidates daily data from two different platforms and calculates aggregated metrics.

## Objectives

The primary objectives of this project are:

1. **Data Consolidation**: Combine data from two tables, `google_ads_basic_daily` and `facebook_ads_basic_daily`, into a unified dataset that includes key metrics for both Google Ads and Facebook Ads.

2. **Metric Aggregation**: Using the consolidated dataset, compute aggregated values of key performance indicators (KPIs) such as total spend, impressions, clicks, and conversion value, grouped by the date of the ad and the media source.

## Project Structure

### 1. Data Sources

- **google_ads_basic_daily**: Contains daily performance data for Google Ads campaigns.
- **facebook_ads_basic_daily**: Contains daily performance data for Facebook Ads campaigns.

### 2. SQL Query Breakdown

#### Step 1: Data Consolidation

Using a Common Table Expression (CTE), the data from both sources is combined. The `media_source` column is manually added to distinguish between the platforms:

\`\`\`sql
WITH combined_ads AS (
    SELECT 
        ad_date, 
        'Google Ads' AS media_source, 
        spend, 
        impressions, 
        reach, 
        clicks, 
        leads, 
        value 
    FROM google_ads_basic_daily
    UNION ALL
    SELECT 
        ad_date, 
        'Facebook Ads' AS media_source, 
        spend, 
        impressions, 
        reach, 
        clicks, 
        leads, 
        value 
    FROM facebook_ads_basic_daily
)
\`\`\`

#### Step 2: Metric Aggregation

The consolidated data is then aggregated to provide daily totals for each platform. This includes summing up the spend, impressions, clicks, and conversion value:

\`\`\`sql
SELECT 
    ad_date, 
    media_source, 
    SUM(spend) AS total_spend, 
    SUM(impressions) AS total_impressions, 
    SUM(clicks) AS total_clicks, 
    SUM(value) AS total_value 
FROM combined_ads
GROUP BY ad_date, media_source
ORDER BY ad_date, media_source
\`\`\`

### 3. Output

The final output provides a comprehensive view of daily advertising performance, with aggregated metrics categorized by the date of the ad and the media source. This output can be further used for reporting, analysis, and decision-making purposes.

## How to Use

To run this project:

1. Ensure you have access to the `google_ads_basic_daily` and `facebook_ads_basic_daily` tables.
2. Copy the provided SQL query and run it in your SQL environment.
3. Review the aggregated results for insights on ad performance.

## Conclusion

This project showcases the power of SQL in data consolidation and aggregation across multiple sources. By applying CTEs and the UNION ALL operator, we effectively combined and analyzed key advertising metrics from Google Ads and Facebook Ads, enabling data-driven decisions.

## License

This project is open-source and available under the [MIT License](LICENSE).

# DannyMA_8thCase_FreshSegments
SQL project


<img width="512" height="523" alt="387157335-2fb16f3a-2015-4bb4-a406-696bdbc366f8" src="https://github.com/user-attachments/assets/c1fa2ca2-a35a-47c3-9499-80956527c1eb" />


🧩 Fresh Segments — Danny Ma (8th Case Study)

Project: Fresh_Segments_DannyMA_8th_Case_Study
Description:
Fresh Segments is a digital marketing agency helping clients analyse trends in online ad-click behaviour.
This case explores how aggregated interest metrics can be used to understand customer engagement and segmentation.
The goal is to clean and analyse monthly interest-based metrics to uncover trends, segment behaviour, and the stability of audience indexes over time.

Datasets:

fresh_segments.interest_metrics → aggregated ad-click & interaction metrics (composition %, index value, ranking)

fresh_segments.interest_map → mapping of interest_id → interest name + metadata

Tools: SQL (PostgreSQL 13), data-cleansing & aggregation, analytical querying

Case Link: 🔗 8 Week SQL Challenge – Case Study #8 (Fresh Segments)

📊 Key Analytical Sections
🔹 Data Exploration & Cleansing

Convert month_year text → date type (first day of month)

Identify null or mismatched IDs between interest_metrics and interest_map

Validate data consistency (month_year vs created_at)

Decide on the correct JOIN strategy and handle missing IDs

🔹 Interest Analysis

Find interests present in all months

Compute cumulative % of records by total_months → identify threshold reaching 90 % coverage

Remove low-occurrence interests (< threshold) and analyse business rationale

Calculate unique interest count per month after filtering

🔹 Segment Analysis

Identify top 10 / bottom 10 interests by maximum composition value

Determine lowest average ranking (5 interests)

Measure highest stdev in percentile_ranking values (5 interests)

Explore min/max ranking trends → interpret customer segment behaviour

Suggest suitable product/service recommendations based on patterns

🔹 Index Analysis

Reverse-calculate average composition for Fresh Segments clients → composition / index_value

Find top 10 interests by avg composition per month

Identify interest appearing most frequently in top 10

Compute monthly average of avg composition

Build a 3-month rolling average (Sep 2018 → Aug 2019) of max composition + top interest

Analyse month-to-month fluctuations and their implications for Fresh Segments’ business model

🧠 Insights & Takeaways

Consistent interests across months → stable customer segments.

High volatility in index values → possible changes in ad targeting or client audience.

Removing rare interest months improves dataset stability.

Combining composition and index metrics reveals where Fresh Segments’ audiences differ from the broader market.

🧾 Sample SQL Starters
-- Convert month_year to date
UPDATE fresh_segments.interest_metrics
SET month_year = TO_DATE(month_year, 'Mon-YY');

-- Record counts per month
SELECT month_year, COUNT(*) AS record_count
FROM fresh_segments.interest_metrics
GROUP BY month_year
ORDER BY month_year;

-- IDs missing from interest_map
SELECT DISTINCT im.interest_id
FROM fresh_segments.interest_metrics im
LEFT JOIN fresh_segments.interest_map mp
       ON im.interest_id = mp.id
WHERE mp.id IS NULL;

-- Join for analysis (validated example)
SELECT m.*, p.interest_name, p.created_at
FROM fresh_segments.interest_metrics AS m
LEFT JOIN fresh_segments.interest_map AS p
       ON m.interest_id = p.id;

💬 Conclusion

The Fresh Segments case study demonstrates how digital marketing analysts use interest-based metrics and index values to detect trends in customer engagement.
It highlights the importance of data cleaning, temporal consistency, and rolling metrics in understanding customer segments and campaign effectiveness.

📚 Credits → Danny Ma – 8 Week SQL Challenge

# Cyclistic Case Study: Strategies to Convert Casual Riders to Annual Members

## Background

Cyclistic, a leading bike-share company in Chicago, has been transforming urban mobility since 2016. With a fleet of 5,824 bicycles and 692 docking stations, Cyclistic offers flexible pricing plans:

- Single-ride passes  
- Full-day passes  
- Annual memberships  

This makes bike-sharing accessible to a wide range of users. Financial analysis has revealed that annual members are more valuable for long-term business sustainability.

As a junior data analyst on the Cyclistic marketing analytics team, my role is to explore historical trip data to uncover insights into how casual riders and annual members use the service differently. These insights will help the marketing team, led by Lily Moreno, design data-driven strategies to convert casual riders into loyal annual members. By identifying key trends, usage patterns, and potential membership incentives, my analysis will provide actionable recommendations that support Cyclistic’s growth objectives and help secure executive buy-in for future marketing initiatives.

## Data License

This public data is provided by Motivate International Inc. under the license available at the following link. To protect user privacy, personally identifiable information about riders is excluded. As a result, it is not possible to link pass purchases to credit card numbers to determine whether casual riders live within the Cyclistic service area or have bought multiple single-ride passes.

## Cyclistic Case Study: Strategies to Convert Casual Riders to Annual Members

### 1. Understanding Usage Patterns: How Casual Riders Differ from Members

#### Overall Ride Volume

- Annual Members: 2,317,410 rides  
- Casual Riders: 1,360,656 rides  

Annual Members take nearly 70% more rides than casual users.

#### Weekly Distribution

- Casual riders peak on weekends (especially Friday-Sunday).  
- Annual Members ride more consistently throughout the week, with a stronger presence on weekdays, especially during commuting hours.

#### Time of Day

- Annual Members ride more during morning and evening commuting hours (6AM-9AM, 3PM-6PM).  
- Casual riders favor midday and evening rides (12PM-3PM, 6PM-9PM), likely for leisure or social activities.

#### Seasonality

- Casual rides spike in warmer months (Q2 and Q3).  
- Annual member usage remains high year-round, with a steady decline only in winter.

#### Popular Routes

- Casual riders prefer scenic, tourist-friendly routes (e.g., Streeter Dr & Grand Ave).  
- Annual Members use more practical, point-to-point routes (e.g., State St & 33rd St) for commuting or errands.

### 2. Why Casual Riders Might Buy a Membership

- **Cost Savings**: Frequent casual riders could save money with a membership, especially those riding more often in peak seasons.  
- **Convenience & Perks**: Exclusive perks like priority bike availability, faster checkouts, or discounts on longer rides could appeal to casual users.  
- **Health & Fitness**: Promoting the health benefits of consistent cycling as part of a lifestyle subscription.  
- **Community & Events**: Hosting member-only events, group rides, or social meetups could encourage community-driven conversion.

### 3. Leveraging Digital Media for Casual Member Conversion

- **Targeted Campaigns**: Use ride data to target high-frequency casual riders with personalized ads showcasing potential savings with a membership.  
- **Social Proof & Testimonials**: Share stories of casual riders who became annual members and enjoyed the benefits.  
- **In-App Prompts**: Offer in-app reminders or pop-ups highlighting membership benefits when casual riders hit a threshold of monthly rides.  
- **Referral & Loyalty Programs**: Encourage current annual members to refer friends with rewards, and offer casual riders a trial membership after a certain number of rides.

### 4. Strategic Recommendations

- **Flexible Membership Plans**: Introduce seasonal or short-term membership options to attract casual riders hesitant about an annual commitment.  
- **Enhanced Weekend Benefits**: Offer weekend-focused membership perks to align with casual riders' habits.  
- **Partnerships & Bundles**: Collaborate with local attractions, gyms, or cafes to offer bundled experiences with membership.

By aligning marketing strategies with the distinct behaviors of casual riders, Cyclistics can increase membership conversions, boost retention, and enhance overall rider satisfaction.

## Data EDA, Cleaning and Analysis for 2024 Cyclistic Ride Data

### 1. Data Collection and Initial Setup

- The dataset consisted of 12 CSV files, each representing a month of ride data for the year 2024.  
- A Python function was developed to merge all monthly data into a single DataFrame, joining on the start datetime to consolidate the dataset for analysis.  
- After merging, the combined dataset contained 5,860,568 entries across 13 columns.

### 2. Initial Data Exploration

The data included start and end dates, start and end locations, rideable types, and membership categories. This provided the foundation for time-based and location-based analyses.

#### Columns found in Raw Data

- ride_id  
- rideable_type  
- started_at  
- ended_at  
- start_station_name  
- start_station_id  
- end_station_name  
- end_station_id  
- start_lat  
- start_lng  
- end_lat  
- end_lng  
- member_casual

### 3. Key Findings and Data Anomalies

- **Rideable Types**: 3 unique rideable types  
- **Membership Types**: 2 categories (member (annual) and casual)

#### Station Data Inconsistencies

- Start station names: 1,808 unique values  
- Start station IDs: 1,763 unique values  
- End station names: 1,815 unique values  
- End station IDs: 1,768 unique values  

This discrepancy raised questions about whether stations had sub-docks or naming inconsistencies.

### 4. Handling Duplicates

- 211 duplicate ride IDs were found, primarily due to millisecond-level timestamp issues.  
- Duplicates were exported to “duplicated_rows.csv” and removed.  
- Milliseconds were truncated for accurate datetime conversion.

### 5. Dealing with Data Quality Issues

- 227 rows with negative durations were exported to “negative_ride_duration.csv” and removed.  
- 496 rows with zero durations were exported to “zer_ride_duration.csv” and removed.  
- 1,651,749 rows had nulls in station names or IDs but not in other fields. These were exported to “null_feilds_data.csv” and removed from the final dataset.

After resolving data issues, the remaining rows were 4,207,975.

### 6. Correcting Location ID and Name Mismatches

- Shared start & end station IDs with multiple names were exported to “start_id_shared.csv” and “end_id_shared.csv”.  
- 26,884 rows had shared station IDs for multiple names.  
- 21,447 public rack entries were corrected and exported to “public_rack_data.csv”.  
- 37 test records were identified and removed, exported as “testing_cycle_data.csv”.  
- 21,540 rows with repeated TA1305000030 IDs were dropped and exported as “ta_id_data.csv”.  
- 6,323 rows with minor location name typos (e.g., "avenue" vs. "ave") were corrected and exported as “minor_name_error_id_data.csv”.

#### Non-Unique IDs

- 260,638 rows had location IDs used across multiple locations, which were exported as “loc_id_dstnct_loc_name.csv” and dropped to preserve data integrity.

### 7. Final Data Preparation

- Rows remaining after cleaning: 3,675,066  
- Exported clean data: "v8_data_for_visualization.csv"

### 8. Feature Engineering

New columns created:

- `month`: Extracted month as an integer  
- `quarter`: Calculated quarter based on the month  
- `ride_distance_km`: Estimated ride distance in kilometers  
- `ride_hour`: Extracted the hour from the start datetime  
- `time_bucket`: Grouped rides into time-based buckets (e.g., 6AM-9AM, 9AM-12AM)

### 9. Final Insights

- Average ride duration:  
  - Casual riders: 25 minutes  
  - Members: 12 minutes

### 10. Tools and Techniques

- **Python**: pandas, numpy, datetime, geopy  
- **SQL**: for shared ID and location analysis  
- **Tableau**: Data visualization and dashboards

#### Data Exports

- Intermediate files were exported for each cleaning stage, preserving traceability  
- Final data exported as “v8_data_for_visualization.csv”

This thorough data cleaning process ensured that the final dataset was well-structured, free of critical inconsistencies, and ready for advanced analytics and visualization.

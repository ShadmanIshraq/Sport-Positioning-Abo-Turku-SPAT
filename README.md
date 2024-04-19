# Sport-Positioning-Åbo-Turku-SPÅT (Description of the Process)
The provided code performs a series of data processing and manipulation tasks using the pandas library in Python. It starts by importing the necessary libraries and then reads two CSV files containing session statistics and position data which are two separate dataframes. These dataframes are subsequently merged based on the 'timestamp' column, resulting in a new dataframe called merged_data.


The merged data is sorted based on the 'player_id' and 'timestamp' columns, and specific columns, such as 'speed' and 'distance,' are removed from the dataset. Unit conversion is applied to two columns ('speed_soft' and 'top_speed'), converting them from meters per second to kilometers per hour.


The code adds two new columns to the dataset: 'player_weight' with a constant value of 38 (because of the unavailability of player weight this constant value 38 is considered) and 'power_output' calculated as the product of 'player_weight,' 'speed_soft,' and a constant factor (1.04). The values in these columns are rounded to three decimal places.


The modified dataset is then saved to an Excel file. In the next part of the code, it reads the previously saved Excel.


In the process of Data Aggregation, the code intelligently organizes the session data by grouping the merged_data dataframe based on the 'player_id.' This grouping serves as the foundation for deriving insightful statistics that provide a comprehensive overview of each player's performance during the session.


The aggregation involves computing key metrics for each player, such as:


Total Time (total_time): This metric is determined by extracting the 'last' timestamp value from the 'twr_timestamp' column for each player. It signifies the overall duration each player spent in the session.


Top Speed (top_speed): Calculated as the maximum value in the 'top_speed' column for each player, this metric captures the highest speed achieved by individual players during the session.


Acceleration Numbers (acceleration_numbers): Representing the number of accelerations for each player, this metric is computed by extracting the 'last' value from the 'acceleration' column.


Deceleration Numbers (deceleration_numbers): Similar to acceleration, this metric denotes the number of decelerations for each player and is derived by considering the 'last' value from the 'deceleration' column.


Speed Exceeded 20 (speed_exceeded_20): Calculated by summing instances where the 'speed_soft' column exceeds 20, this metric quantifies the count of occurrences where players surpassed a speed threshold of 20.


Total Distance (total_distance): This metric is obtained by extracting the 'last' value from the 'distance_soft' column, signifying the cumulative distance covered by each player.


Powerplay Count (powerplay_count): Indicating instances where power output exceeds 500, this metric is computed by summing occurrences where the 'power_output' column surpasses the specified threshold.


Subsequently, in Excel Output, the aggregated data is systematically stored in a new Excel file, the path of which is specified by the variable output_file_path. Notably, the index information is included in the Excel file, providing a structured and comprehensive representation of the aggregated session statistics for further analysis or reporting.
# Workflow of the code
Import Libraries: The code begins by importing the necessary library, pandas, and assigning it the alias 'pd.'


File Paths: Reads two CSV files of a session, one is the statistic data of the session and the other one is position data of the session.


Data Loading: The code uses pandas to read the CSV files into two separate dataframes, data1 and data2.


Data Merging: The dataframes are merged using the 'timestamp' column with an inner join, creating a new dataframe called merged_data.


Sorting: The merged data is sorted based on the 'player_id' and 'timestamp' columns.


Columns Deletion: Specific columns ('speed', 'distance', 'timestamp', 'session_id', 'session', 'x', 'y', 'tag_id.1') are dropped from the merged data.


Unit Conversion: Two columns, 'speed_soft' and 'top_speed,' are converted from meters per second to kilometers per hour (3.6 times the original values), rounded to three decimal places.


Column Additions: Two new columns, 'player_weight' and 'power_output,' are added to the merged data. 'player_weight' is assigned a constant value of 38, and 'power_output' is calculated based on the product of 'player_weight,' 'speed_soft,' and a constant factor (1.04), rounded to three decimal places.


Excel Output: The modified merged data is saved to an Excel file.


File Paths (Continued): Reads the modified merged data from the output of the previous code cell.


Data Aggregation: Groups the merged_data dataframe by 'player_id' and aggregates various statistics like 'total_time,' 'top_speed,' 'acceleration_numbers,' 'deceleration_numbers,' 'speed_exceeded_20,' 'total_distance,' and 'powerplay_count' using different aggregation functions.


'total_time'=('twr_timestamp', 'last'): It calculates the 'last' value of the 'twr_timestamp' column for each player, representing the total time for each player.
'top_speed'=('top_speed', 'max'): It calculates the maximum value of the 'top_speed' column for each player, representing the top speed achieved by each player.
'acceleration_numbers'=('acceleration', 'last'): It calculates the 'last' value of the 'acceleration' column for each player, representing the number of accelerations for each player.
'deceleration_numbers'=('deceleration', 'last'): It calculates the 'last' value of the 'deceleration' column for each player, representing the number of decelerations for each player.
'speed_exceeded_20'=('speed_soft', lambda x: (x > 20).sum()): It calculates the sum of occurrences where the 'speed_soft' column is greater than 20 for each player, representing the count of instances where the speed exceeded 20 for each player.
'total_distance'=('distance_soft', 'last'): It calculates the 'last' value of the 'distance_soft' column for each player, representing the total distance covered by each player.
'powerplay_count'=('power_output', lambda x: (x > 500).sum()): It calculates the sum of occurrences where the 'power_output' column is greater than 500 for each player, representing the count of instances where the power output exceeded 500 for each player.


Excel Output (Continued): The aggregated data is saved to a new Excel file specified by the variable output_file_path. The index is included in the Excel file.

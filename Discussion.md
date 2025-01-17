Why This Solution Is Efficient
Binary Search: Instead of sequentially scanning from the beginning (which could take hours on a huge file), you skip around to find where the date starts. Each seek/read is logarithmic in terms of the file size.
Streaming Read: After finding the start position, you process lines one by one, so memory usage remains low.
Immediate Stop: Once you see a line that no longer matches target_date, you stop reading—no need to parse the rest of the file.
This combination addresses both time and memory efficiency.
Comparison to Other Approaches
Naive Approach: Doing grep "2024-12-01" test_logs.log would read the entire file from start to finish. This might be okay for a 1–2 GB file, but not for multi-hundred-GB or TB-scale logs.
Single-Pass Approach (sequential read from the start): Also O(n) in file size—inefficient if your date is near the end.
Index-Based Approach:
If you had to run many repeated queries, you might do a preprocessing step building a date → byte-offset index. Then each query is a single seek plus minimal scanning.
However, building/maintaining that index is more complex.
This Code’s Approach is a nice middle ground—no preprocessing required, but still beneficial for a single or occasional date query.
HOW to run-
Clone or Download the Repository

Clone the GitHub repository containing the extract_logs.py script.
Navigate to the Project Directory

In your terminal, move into the directory where extract_logs.py is located.
Check for the Log File

Ensure that the logs_2024 exists in the same directory as the script, or adjust the log_file variable in the code to point to its location.Run the Script

Provide the target date (YYYY-MM-DD) as a command-line argument, for example:
bash
Copy
python extract_logs.py 2024-12-01

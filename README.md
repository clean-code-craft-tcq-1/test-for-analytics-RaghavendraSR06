# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Library to read the CSV file
3. Library to generate the PDF report
4. Library to send notification (ex: Email notification) 
5. Library to perform read/write operations on File

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | For converting the report to PDF
Counting the breaches       | Yes           | To count the number of breaches
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | Sending the notification on monthly basis

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "No minimum value" to the PDF when the csv does not contain defined minimum values.
4. Write "No maximum value" to the PDF when the csv does not contain defined maximum values.
5. Write "Number of breach count" to the PDF when the breach count crosses the defined threshold.
6. Write "Not Breached" to the PDF when the values does not cross defined threshold value.
7. Write "File Not Found" if the PDF not available in the defined location.
8. Write "File Not Found" if the CSV is not available in the defined location.
9. Write "Connection Error" if there is any connection related issue.
10. Write "No new report generated" if there is no new report generated for the week.
11. Write "Notified Succesfully" when the PDF is reported(notified) successfully.
12. Write "No Trends available" if there is no continous increase in the csv data.
13. Write "invalid Data" if special characters are available in the CSV File.

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input           | Output                                                    | Faked/mocked part
|--------------------------|-----------------|-----------------------------------------------------------|------------------
Read input from server     | csv file        | internal data-structure                                   | Fake the server store
Validate input             | csv data        | valid / invalid                                           | None - it's a pure function
Notify report availability | New PDF Report  | Notification to the target                                | Fake the notify
Report inaccessible server | Conn_error(404) | Display connection issue                                  | Fake the server
Find minimum and maximum   | csv file        | report of minimun and maximum value                       | None - it's a pure function
Detect trend               | CSV file        | report of readings in 30 mins                             | mock the readings
Write to PDF               | CSV file values | Minimum,Maximum,Count of breaches and trends from csv file| mock the PDF output

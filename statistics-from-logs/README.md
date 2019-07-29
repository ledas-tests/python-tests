# Statistics from logs

## Goal

The goal is to extract some information from the log files that are generated during execution of the test cases and present this information as a table with one row for each test case.

## Structure of directories with log files

During the execution of test cases the log files are generated in the following structure:

```
output-dir
├───test-case-0
│   ├───test-case-0.log
│   ├───test-case-0-00.data
│   ├───test-case-0-01.data
│   ...
├───test-case-1
│   ├───test-case-1.log
│   ├───test-case-1-00.data
│   ├───test-case-1-01.data
│   ...
...
```

For each test case directory with its name is created. Inside this directory the log file is generated with the name equal to the directory and extension `.log`. Also some other additional files are generated in the test case directory like the ones with `.data` extension in the example above.

## Structure of log file

Log file for the test case has a simple structure like this:

```
14:45:50.159963] spurn marsala cushy drove emic hows migs
14:45:50.439963] once furans nocks gable brulots doge
14:45:56.674963] Statistics: 13 9 2 1 7
14:45:57.282963] vapor pas bespoke induced you press wen men
14:46:01.647963] etch wyles tag dromond ka if infest myc footies
14:46:04.400963] Statistics: 5 13 14 8 6
14:46:05.075963] fe mozo stomas aioli bauds
14:46:06.252963] posit jab cull hurly ceorl
```

Each line contains a log message. We are interested in specific messages that contain `Statistics:` string with some integer numbers after the colon. It is expected that for each test case and each message we have the same number of integers. For particular test case we are interested in the sums of integers by all the messages with statistics. For example in the log shown above we need to sum integers from two messages: `Statistics: 13 9 2 1 7` and `Statistics: 5 13 14 8 6`, we will have `13+5 9+13 2+14 1+8 7+6` or `18 22 16 9 13`. This is the information we need present in the row of table for the test case.

## Representation of collected statistics

After extraction of statistics from log files for all the test cases we need to represent it in the form of table like this:
```
-------------------------------------------------------
| Name   | Stat 0 | Stat 1 | Stat 2 | Stat 3 | Stat 4 |
-------------------------------------------------------
| vinos  |    122 |     79 |    117 |    129 |    112 |
| diners |    120 |     77 |     67 |    124 |    107 |
| winker |    109 |    112 |    120 |     56 |    133 |
| annona |     95 |     91 |    111 |     77 |    109 |
-------------------------------------------------------
```
Where the first column contains test case name and all other columns  contain statistics numbers for the test case extracted from the log file.

Additionally we expect this table to be sorted by `Stat 0` column in descending order (we interpret first statistics number as the most important one and want to sort all the test cases by this parameter).

## Expected

As a result we expect a link to GitHub repository with python script. The script should take one argument: the path to directory with logs, and it should print the table with results to `stdout`. Any third-party libraries can be used but in such case some instruction about installing them is expected.

## Examples of logs

Examples of output directories with log files can be found [here](./example-logs).

## Feedback

Any questions related to this task can be asked via creating GitHub issues for this repository.

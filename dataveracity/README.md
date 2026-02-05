# Data Veracity Example
This example shows how to use Data Veracity. An example configuration hosted on our github example repository. These consist of 2 Ultra Format Definition files, 1 forwarding workflow, 1 collection workflow, 1 Database profile and 1 Data Veracity profile. 

Data Veracity Forwarding Workflow:

**Disk In --> Decoder --> Analysis --> Data Veracity Forwarder**

| Agent |	Description |
|-------|-------------|
| Disk In | Collects the data file |
| Decoder | Decodes the sample data file |
| Analysis | Check the causeForOutput field is not 0 and forwards the record to Data Veracity Forwarder |
| Data Veracity Forwarder | Forwards the records into the Data Veracity table |

Data Veracity Collection Workflow:

**Data Veracity Colletor --> Analysis --> Encoder --> Disk Out**
                                    **--> Data Veracity Forwarder**

| Agent |	Description |
|-------|-------------|
| Data Veracity Collector | Collects the records for reprocessing from the Data Veracity table |
| Analysis | Check the causeForOutput field is 1 and forwards the record to the encoder. Any other value gets forwarded to Data Veracity Forwarder |
| Encoder | Encodes the reprocessed records |
| Disk Out | Writes the record into a file and stores it in a local file system |
| Data Veracity Forwarder | Forwards the records into the Data Veracity table |

## Sample Data
Paste the data into an empty text file.

A:1,112233,445566,1,5<br>
A:2,112233,445566,1,6<br>
B:3,999999,888888,1,10<br>
A:4,112233,445566,2,9<br>
C:5,333333,111111,1,10<br>
C:6,333333,111111,2,100<br>
B:7,999999,888888,1,12<br>
D:8,111111,222222,1,3<br>
D:9,111111,222222,1,31<br>
D:10,111111,222222,2,4<br>
E:11,333333,444444,1,55<br>
X:12,222233,445566,0,5<br>
X:12,222233,445566,0,5<br>
X:13,999999,888888,0,10<br>
X:14,112233,445566,0,9<br>
X:15,333333,111111,0,10<br>
X:15,333333,111111,0,10<br>
X:16,999999,888888,0,2<br>
X:17,991111,222222,0,3<br>
X:18,331111,222222,0,3<br>
X:19,441111,222222,0,4<br>
X:20,333333,444444,0,5<br>
X:21,436890,546781,0,9<br>
X:22,121212,101010,0,8<br>
X:23,747474,919191,0,3<br>
X:24,123123,456456,0,5<br>
X:25,878787,131313,8,8

## Import
To import the workflow example use the mzcli command line tool

mzcli <user>/<password> systemimport <export-dir>

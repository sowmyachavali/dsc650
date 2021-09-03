---
title: Assignment 1.2
subtitle: Computer performance, reliability, and scalability calculation
author: Sowmya Chavali
---

#### a. Data Sizes

| Data Item                                  | Size per Item | 
|--------------------------------------------|--------------:|
| 128 character message.                     | 128 Bytes     |
| 1024x768 PNG image                         | 1.1 MB        |                                 
| 1024x768 RAW image                         | 1.5 MB        | 
| HD (1080p) HEVC Video (15 minutes)         | 156.43 MB     |
| HD (1080p) Uncompressed Video (15 minutes) | 156430 MB     |
| 4K UHD HEVC Video (15 minutes)             | 2550 MB       |
| 4k UHD Uncompressed Video (15 minutes)     | 2550000 MB    |
| Human Genome (Uncompressed)                | 1.5 GB        |


#### 1024x768 PNG image
If use RGB, each pixel(Red Blue and Green channels) in the image needs 3 bytes in memory.
So the total file size 1024*768*3=2,359,296 bytes= 2,359296/1024/1024=2.25MB. 
PNG is compressed, atypical compression ratio is 2,then the size is about 1.1 MB 
https://www.scantips.com/basics1d.html 
#### 1024x768 RAW image
((1024*768)*16)/8/1024/1024 = 1.5Mb
https://4nsi.com/faq/how-do-i-calculate-the-file-size-for-a-digital-image
#### HD (1080p) HEVC Video (15 minutes)
156430/1000 MB= 156.43
#### HD (1080p) Uncompressed Video (15 minutes)
156.430GB * 1000 = 156430 MB
https://www.digitalrebellion.com/webapps/videocalc?format=uncompressed_8_1080&frame_rate=f30&length=15&length_type=minutes
#### 4K UHD HEVC Video (15 minutes) 
We are considering shooting in 4K at 30FPS with your iPhone, here's how much it space it'll take up on your device for 15 mins.
170MB * 15 = 2550MB
https://www.imore.com/how-shoot-trim-edit-and-share-4k-video-iphone
#### 4k UHD Uncompressed Video (15 minutes)  
2550*1000 = 2550000 MB
#### Human Genome (Uncompressed)  
6*10^9 base pairs  genome x 1 byte/4= 1.5GB (https://bitesizebio.com/8378/how-much-information-is-stored-in-the-human-genome/)

#### b. Scaling
|                                          |  Size     | # HD | 
|------------------------------------------|----------:|-----:|
| Daily Twitter Tweets (Uncompressed)      |  192 GB   |    1 |
| Daily Twitter Tweets (Snappy Compressed) |  127.98 GB|    1 |
| Daily Instagram Photos                   |  236.01 TB|   24 |
| Daily YouTube Videos                     | 1351.56 TB|  136 |
| Yearly Twitter Tweets (Uncompressed)     |   70.08 TB|    8 |
| Yearly Twitter Tweets (Snappy Compressed)|   46.71 TB|    5 |
| Yearly Instagram Photos                  | 86143.65TB| 8615 |
| Yearly YouTube Videos                    |493319.4 TB|49332 |

#### Daily Twitter Tweets (Uncompressed)
Max tweet length is 280. Assuming 128 is the average tweet length. 
Number of tweets per day as of 2020 -> 500 million
Size = 500 million * 128 bytes = 64 GB
We are storing the data using HDFS. By default, HDFS stores three copies of each piece of data, so you will need to triple the amount storage required.
Size= 64*3 = 192 GB
#HD = 1 AS Size < 1TB
https://www.dsayce.com/social-media/tweets-day/
#### Daily Twitter Tweets (Snappy Compressed)
Snappy compression ratio is 1.5-1.7x for plain text. 
Size = 64/1.5 = 42.66GB
tripling the Storage, Size = 42.66*3 = 127.98GB
#### Daily Instagram Photos
Instagram statistics estimates over 100 million videos and photos are uploaded to Instagram every day. 
Assuming that 75% of those items are 1024x768 PNG photos.
75 million photos x 1.1 MB per photo = 82.5 million MB / 1024 = 80566 GB / 1024 = 78.67 TB. 
78.67 TB x 3 copies = 236.01 TB / 10 TB per HD = 23.601 HD ~ 24 hard drives.
#### Daily YouTube Videos
YouTube statistics estimates 500 hours of video is uploaded to YouTube every minute. 
We assume all videos are HD quality encoded using HEVC at 30 frames per second.
Daily upload hours 500*60*24 = 720000 hrs 
HEVC Video (15 minutes) size/hr - 156.43 MB * 4 = 625.72 MB
daily videos size = 720000 * 625.72 = 450518400 Mb ~ 450.52 TB
Making 3 copies = 450.52 TB * 3 = 1351.56
1351.56 TB/10 TB ~ 136
#### Yearly Twitter Tweets (Uncompressed)
64 GB (daily) * 365 = 23360 GB = 23.36 TB
Size for 3 copies = 70.08 TB
HD count= 70.08TB/10TB  ~ 8 
#### Yearly Twitter Tweets (Snappy Compressed)
42.66 GB(daily) * 365 = 15570.9 GB = 15.57 TB
Size for 3 copies = 46.71 TB
HD count = 46.71/10 TB ~ 5
#### Yearly Instagram Photos
78.67 TB (Daily) * 365 * 3 copies = 86143.65 TB
HD = 86143.65 / 10 TB = 8615
#### Yearly YouTube Videos
450.52 TB (daily) * 365 * 3 copies = 493319.4 TB
HD = 493319.4 TB / 10 = 49332

#### c. Reliability
|                                    | # HD | # Failures |
|------------------------------------|-----:|-----------:|
| Twitter Tweets (Uncompressed)      |    8 |         1  |
| Twitter Tweets (Snappy Compressed) |    5 |         1  |
| Instagram Photos                   | 8615 |        88  |
| YouTube Videos                     |49332 |       499  |

annualized failure rate(Q2 2021) = 1.01% (https://www.backblaze.com/b2/hard-drive-test-data.html)
0.0101 * 8 = 0.0808 ~ 1 (Rounding the failures to numbers)
0.0101 * 5 = 0.0505 ~ 1
0.0101 * 8615 = 87.0115 ~ 88
0.0101 * 49332 = 498.2532 ~ 499

#### d. Latency
|                           | One Way Latency      |
|---------------------------|---------------------:|
| Los Angeles to Amsterdam  |  70.8 ms             |
| Low Earth Orbit Satellite |  20 ms               |
| Geostationary Satellite   | 300 ms               |
| Earth to the Moon         |1280 ms               |
| Earth to Mars             |  20 minutes          | 


#### Los Angeles to Amsterdam  
 141.655ms RTT/2 = 70.8 ms
 https://wondernetwork.com/pings
#### Low Earth Orbit Satellite 
 RTT/2 = 40/2= 20 ms -> one way latency
#### Geostationary Satellite  
 600/2 = 300 ms -> one way latency
 https://www.omniaccess.com/leo/#:~:text=The%20GEO%20latency%20is%20of,and%20an%20essential%20part%20if
#### Earth to the Moon 
2.56 seconds /2 -> 1.28 sec one way
https://en.wikipedia.org/wiki/Earth%E2%80%93Moon%E2%80%93Earth_communication#:~:text=Propagation%20time%20to%20the%20Moon,milliseconds%20of%20wave%20travel%20time.
#### Earth to Mars
https://mars.nasa.gov/mer/mission/timeline/surfaceops/navigation/

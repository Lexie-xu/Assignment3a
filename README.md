# Elon Musk's tweets dataset
## Description of the dataset
This dataset contains Elon Musk's tweets from 2010-06-04 to 2017-04-05, including columns such as 'id', 'created_at', 'text', and 'year'.
|   id   |      created_at      |                                               text                                               | year |
|-------|----------------------|--------------------------------------------------------------------------------------------------|------|
|  494  | 2016-11-04 16:15:43  |  @MrRoryReid @MykalSoCal @BBC_TopGear @TeslaM...  | 2016 |
| 1878  | 2014-05-23 23:47:45  |  @westcoastbill First, the cheese. Then, the ...  | 2014 |
| 1135  | 2016-04-03 21:47:19  |  @GolfsHard yes  | 2016 |
| 2803  | 2011-12-22 11:30:10  |  Model S options are out! Performance in red ...  | 2011 |
| 1329  | 2015-12-19 00:09:39  |  Static fire test looks good. Pending data re...  | 2015 |
|  259  | 2017-02-04 17:03:52  |  In addition, I again raised climate. I belie...  | 2017 |
| 1070  | 2016-04-20 01:36:45  |  @RealDarthBL We have amplified pre-delivery ...  | 2016 |
| 1073  | 2016-04-17 22:34:35  |  Owner video of Autopilot steering to avoid c...  | 2016 |
| 1092  | 2016-04-08 21:17:01  |  @NASA @sgvcrime @SpaceX @Space_Station Thank...  | 2016 |
|   34  | 2017-03-28 16:57:18  |  @nickg_uk @chouky02 You won't care  | 2017 |

## Questions and Visualization
### Conditional Selection
#### Among all Musk's tweets, find 20 tweets that contain the keyword 'Tesla'.
```keyword = 'Tesla'```

We select the tweets that contain 'Tesla' and display the first 20 entries in the result, including the columns 'year' and 'text'.
```
tweets_with_keyword = data[data['text'].str.contains(keyword, case=False)].head(20)[['year', 'text' ]]
print(tweets_with_keyword)
```
|  year |                                               text                                               |
|-------|--------------------------------------------------------------------------------------------------|
| 2017  |  @ForIn2020 @waltmossberg @mims @defcon_5 Example of how the autopilot safety features look in the car |
| 2017  |  @tesla_addict @TeslaMotors Working on it |
| 2017  |  Made today on Tesla sketch pad https://t.co/... |
| 2017  |  @business Glad to have Tencent as an investor |
| 2017  |  RT @arctechinc: @elonmusk we believe so much... |
| 2017  |  RT @Herifin_teki: @elonmusk My lil monster T... |
| 2017  |  RT @RicardoTwumasi: @elonmusk My Tesla Model... |
| 2017  |  RT @Shkottt: @elonmusk my Tesla Roadster is ... |
| 2017  |  @Skate_a_book Yes. Model S will always be th... |
| 2017  |  @luciojr All Tesla cars built since Oct last... |
| 2017  |  Am noticing that many people think Model 3 i... |
| 2017  |  @mcannonbrookes $250/kWh at the pack level f... |
| 2017  |  @mcannonbrookes Tesla will get the system in... |
| 2017  |  RT @TeslaMotors: Project Loveday https://t.c... |
| 2017  |  Excellent Tesla Model X review https://t.co/... |
| 2017  |  In appreciation, Tesla is providing all repa... |
| 2017  |  Congrats to the Tesla owner who sacrificed d... |
| 2017  |  @SEACityLight @Nas2four Sounds like the Tesl... |
| 2017  |  @RusulAlrubail @MarkRuffalo @guardian Please... |
| 2017  |  RT @TeslaMotors: Supercharger availability I... |

#### Filter out 10 tweets that Elon Musk posted in 2016.
We first filter for the year equal to 2016 and display the first 10 results, including the columns 'year' and 'text'.
```
tweets_2016 = data[data['created_at'].dt.year == 2016].head(10)[['year', 'text']]
print(tweets_2016)
```
|  year |                                               text                                               |
|-------|--------------------------------------------------------------------------------------------------|
| 2016  |  HW2 Autopilot software uploading to 1000 car... |
| 2016  |  @vicentes @DragTimes Late Jan, along with Li... |
| 2016  |  @DragTimes Yes, but held up by Autopilot . I... |
| 2016  |  Resolving an Autopilot HW2 bug that shows up... |
| 2016  |  Churchill (non) quotes \nhttps://t.co/avA4YD... |
| 2016  |  RT @IridiumComm: Milestone Alert: The first ... |
| 2016  |  @andrewket Almost there. Undergoing final va... |
| 2016  |  RT @ElectrekCo: Tesla Autopilot\xe2\x80\x99s... |
| 2016  |  Deus ex machina on the center screen when it... |
| 2016  |  @quipme Occasional existential dread is inev... |

### GROUP BY() function
#### What is the average length of Elon Musk's tweets for each year?
We can create a new column called 'tweet_length'.
```
data['tweet_length'] = data['text'].apply(len)
```
We first group data by year.
```
group_by_year = data.groupby(data['year'])
```
We will calculate the average tweet length for each group.
```
avg_tweet_length_per_year = group_by_year['tweet_length'].mean().reset_index()
print(avg_tweet_length_per_year)
```
|  year | tweet_length |
|-------|--------------|
|  2010 |     95.000   |
|  2011 |    114.932   |
|  2012 |    108.921   |
|  2013 |    106.205   |
|  2014 |    103.224   |
|  2015 |    103.507   |
|  2016 |     94.261   |
|  2017 |     94.172   |
### Visualizing the trend of Musk's tweet count over time
```
import matplotlib.pyplot as plt
```
Firstly, convert the column to datetime format.
```
data['created_at'] = pd.to_datetime(data['created_at'])
```
Then we group the data by year and calculate the number of tweets per year.
```
tweets_per_year = data.groupby('year').size()
```
In the end, we create a figure to show the result.
```
plt.figure(figsize=(10, 6))
tweets_per_year.plot(kind='bar', color='skyblue')
plt.title('Elon Musk Tweets Over the Years')
plt.xlabel('Year')
plt.ylabel('Number of Tweets')
plt.show()
```
![image](https://github.com/Lexie-xu/Assignment3a/blob/main/Elon%20Musk%20Tweets%20Over%20the%20Years.png)
#### What conclusion can we infer from this bar chart?
The results indicate a significant increase in Musk's tweet volume in 2016. This is likely attributed to substantial progress made by Musk's companies in various aspects. This surge in tweet activity suggests active promotion and engagement on Musk's part. For instance, notable events include:
1. Tesla's official launch of the new electric car, the Model 3, in July 2016.
2. The completion of Tesla's acquisition of solar energy company SolarCity in November 2016.
3. SpaceX's successful vertical landing of the Falcon 9 rocket.
4. Introduction of the ambitious 'Interplanetary Spaceship' plan
# Source of the dataset
Created by @adamhelsinger

Note from Project Team: There are multiple files in our GitHub repository, as we worked through various aspects of the project. The ones you need to review are:
- Team 8 Presentation Final.pptx (https://github.com/iabdullah42/Project_1/blob/main/Project_1/Team%208%20Presentation%20Final.pptx)
- Group8_BLS_API_notebook.ipynb (https://github.com/iabdullah42/Project_1/blob/main/Project_1/Group8_BLS_API_notebook.ipynb)
- This README (https://github.com/iabdullah42/Project_1/edit/main/README.md)

*All visualizations are provided in our code and within the presentation. Within our presentation, we discuss the more macro views of the industries; however, within our appendix we illustrate the additional visualizations which include seasonality and COVID which is referenced in our analysis.*


# Project Title: Exploration of Computer Science Jobs in the United States #

## Group 8 (Ab Ibrahim, Albwin "Al" Wagner-Schmitzer, Del Vinas, Jay Howarth, Crystal White) ##

## Submission Date: January 11, 2023 ##

### Sections Included ###
-	Section 1. How We Approached the Project
-	Section 2. How We Approached the Data Sourcing, Manipulation, & Analysis
-	Section 3: What We Learned
-	Section 4: Conclusion
-	Section 5. Remaining Questions for Future Exploration
-	Section 6. References
-	Section 7. Code Documentation

### Section 1: How We Approached the Project ###

During our first class, we discussed the project requirements and various public data sources, ultimately deciding on the Bureau of Labor Statistics. We chose this data source because we thought it would be interesting and useful to understand how jobs within artificial intelligence field have changed, particularly over the past 2 years. We spent quite a bit of time in the first 2 classes combing through the BLS data, which, although it’s both broad and extensive, what it is not is architected in a way that any single human being could easily find and make use of that data which presented us some challenges and required pivots along the way (which is discussed later in this report).
                
### Section 2: How We Approached the Data Sourcing, Manipulation, & Analysis ###

**Overview**

As a group, we split up various duties which included project requirement review, documentation, presentation creation, review of BLS data tables, code research, experimentation, and testing. We also met outside of class and explored various data sources and questions we could answer with the data. And, that’s when we hit our first snag.

Our initial research question was to define what is happening within the field of artificial intelligence in terms of employment, but we quickly learned that the BLS does not separate “artificial intelligence” as its own occupation subcategory. Instead, the BLS categorizes those employed in computer science fields as under one of a number of NAICS codes, primarily 15-1210, 15-1250, 15-2041, 15-2051. We learned that “artificial intelligence” has only shown up as a self-reported occupation since 2000, so it has not yet grown to such a degree that BLS categorizes it separately, but that may well change in the near future, as discussed later in this report (Council of Economic Advisors, 2022). 

Since our original hypothesis could not be supported with the BLS data, we pivoted to view the “computer science” occupation designation which would include people working in artificial intelligence, machine learning, and data science. While further exploring that segment of data, we decided that rather than just reporting on job growth within computer science, what we wanted to demonstrate for our class members was which industries in the United States have the greatest number of real jobs, such that when our classmates begin building their resumes and portfolios, they can consider tailoring their application to the highest-growth industries. 

And, even though we had our plan for how to source and analyze the BLS data such that it met the project requirements, we still wondered if we could provide more granularity around the number of artificial intelligence jobs in the U.S., even as additional information to supplement the BLS data exploration. To support this supplementary request, we explored a new product, Kadoa, and scheduled time with a co-founder to discuss how to pull in jobs data from Indeed, LinkedIn, and potentially connecting their product to BLS data. We also pulled additional reports provided by the White House, government agencies, and credible news sources. 

To be efficient as a group, we pulled down the tables of data to review which industries employed the largest number of computer scientists. Those industries were: Government, Health and Education, Financial Services, Retail, Professional and Business Services, and Manufacturing industries. With our plan of industries to target, we were prepared to start pulling in the data for analysis. 

**Getting into the Code**

We began setting up our code by defining the API and keys needed to call in the BLS data. Now, at this point we ran into our 2nd challenge: Figuring out how to build the Series IDs needed to call the data we needed because the only instructions the BLS gives on how to use their Series IDs is to state, “A catalogue of Series IDs is not yet available.” So, the five of us dug around on the internet, queried ChatGPT, Bard, and even reached out to BLS statisticians on LinkedIn to try to figure out how to build the Series IDs. 

Fortunately, after 40 minutes and much frustration, Al figured out that the Series IDs are created by cobbling together multiple types of information as follows: Field Names, Prefix, Seasonal Adjustment Codes, Industry Codes, and Data Type Codes. Each of the fields must be input in a certain position to build the correct Series ID. So, finally having solved that piece of the puzzle (with no help from BLS documentation), we were ready to actually start coding.

We defined our time series as beginning in 2015 and ending in 2024 (with projections extending into 2027). We wanted to illustrate the data leading up to present but also to predict what could be a change in employment across industries in a near future, preferring to stay closer to present to have a more accurate forecast. 

Documentation of our code can be found in “Section 7. Code Documentation.” Due to the extensiveness of our documentation, we thought it would make for a better reader experience to provide the findings first, then let you review the documentation for the code later. 

---


### Section 3: What We Learned ###

**Key Learnings from the Data**

*Overview*

-	**Government** Full-time employment in the government industry was trending slightly upwards until 2020 when COVID hit, dropping to its lowest number of full-time employees since before 2015, and has not yet returned to pre-COVID levels.


-	**Health and Education** Similar to the government, overall employment was trending upwards until 2020; however, job loss was not as significant as it was in the government industry, and it recovered much faster, reaching pre-pandemic levels by early 2023.


-	**Financial Activities** Within the industry of finance, we see significantly fewer jobs overall than in Government and Health and Education sectors; however, the employment trends are similar to these other industries in that employment was trending upwards, dipped in 2020 (with a loss of less than 500,000) jobs, before reaching and exceeding pre-pandemic levels in 2021.

-	**Retail Trade** Overall, the Retail industry employs fewer full-time workers than either the Government or Healthcare and Education industries but more people are employed than within the Financial industry. Unlike the previously discussed industries, Retail employment was declining previous to 2020 and may not yet reach 2019 employment levels until this year.

-	**Professional and Business Services** With Professional and Business Services, we see similar overall employment numbers to Government and Health and Education, but we also see a swift post-pandemic recovery period similar to the Financial industry, reaching pre-pandemic employment levels mid-2021.

-	**Manufacturing** At a peak of 13,000,000 full-time employees in 2019, manufacturing employs the 2nd lowest number of FTEs from the industries we’ve reviewed, but unlike Financial Services, Manufacturing didn’t reach pre-pandemic employment levels until 2023 and is expected to increase by less than 1,000,000 jobs by 2027. 

*Government*

Full-time employment in the government industry was trending slightly upwards until 2020 when COVID hit, dropping to its lowest number of full-time employees since before 2015, and has not yet returned to pre-COVID levels. Looking more closely at the data, we can see a trend in the government industry where there is a seasonal dip every year mid-way through the calendar year. A second, lesser dip can be observed occurring at the beginning of every calendar year. This makes sense when considering that federal and state governments operate on an annual budget which typically begins in July of each year, is re-evaluated at the mid-point at each fiscal year, then wraps up at the end of each June. Specifically, we observe that starting in July, there is an acceleration of hiring which drops off slightly at the end of the calendar year before picking back up in the months of February to April before taking a dip in May, then experiencing a steeper decline every June. 

Using Prophet, we forecast full-time employment within the government throughout the 2026 calendar year. What we see from the data is that there is an expected steady increase in employment, year over year, adding more than 1,000,000 of full-time employees by the end of 2026.

When we looked at the values on an annual basis, using Prophet, we noticed that there was a steep decline at the end of February which caused us to look more closely at the raw data. From review of the data tables, the decline didn’t seem to match our chart. So, we considered what could be creating the unexpected decline across all of our industries (not just Government). To get help understanding what we may need to correct, we reached out on LinkedIn to people working at Meta who listed Prophet in their profile. A program manager who had worked with Prophet replied to our message, connected us with Prophet’s Data Science Manager, who provided some feedback on where we needed to correct our approach. 

What we learned was to use the "holidays" function in Prophet to account for the period of time when COVID layoffs happened which is reflected in the yearly trend. Once we'd adjusted the model, we found a clearer visualization of the seasonality of the government industry with a decline happening each June to July with a lesser decline happening end of year, while still observing the affect COVID had on the Government industry.

In our presentation, we demonstrate the difference the new model made in Slide 15: "Healthcare and Education Industry" which is covered in the next section.

*Health and Education*

Similar to the government, employment was trending upwards until 2020; however, job loss was not as significant as it was in the government industry, and it recovered much faster, reaching pre-pandemic levels by early 2023. Pre-pandemic, overall employment within the Health and Education industries was higher than that of the government industry (by almost 2,000,000). 

Using Prophet to forecast job growth within the health and education industries, what we see is that almost 4,000,000 more jobs will be created within these industries for the time period from 2024-2027. This trend is further reflected by a table provided by the BLS which shows that Healthcare Services is the highest growth industry in terms of employment, and, at roughly 15% annual growth, is the only area expected to have the same double-digit growth in jobs as “Computer Science and Mathematics” (Bureau of Labor Statistics, 2023).  Notably, Computer Science and Mathematics” jobs have an annual median income of $100k whereas “Health Care Services” has an annual median income of $33k. But, let’s get back to the Prophet data visualizations.

For the Healthcare and Education industry, what we learned about seasonality is that the steepest decline in employment happens just before May before continuing a trend upwards until end of year. Before we revised the model the steepest decline seemed to happen just before March. There is a decline during that time, representative of COVID layoffs, but by changing our model, we could see the true seasonality of employment within Healthcare and Education. 


*Financial Activities*

Within the industry of Finance, we see significantly fewer jobs overall than in Government and Health and Education sectors; however, the employment trends are similar to these other industries in that employment was trending upwards, dipped in 2020 (with a loss of less than 500,000) jobs, before reaching and exceeding pre-pandemic levels in 2021.

Although employing far fewer full-time employees than either Healthcare and Education or Government industries, the Financial Services industry recovered more quickly and has been growing at a steady rate since its recovery in 2021. Projecting from 2024 to 2027, our model shows that employment in the Financial Services industry is expected to increase by 500,000 jobs, as a conservative estimate. 

In reviewing seasonality in the "yearly" model, we see that Financial Activities has a steep decline in March and another, lesser steep decline just before May. Financial activities then seems to pick up significantly, then experiencing some lesser ups and downs, recovering just after January of each year. 

*Retail Trade*

Overall, the Retail industry employs fewer full-time workers than either the Government or Healthcare and Education industries but more people are employed than within the Financial industry. Unlike the previously discussed industries, Retail employment was declining previous to 2020 and may not yet reach 2019 employment levels until this year.

The volatility of the Retail industry can be observed through our visualizations with seasonal heights being reached at the end of each year (which is expected due to holiday shopping); however, when the data is viewed outside of the end-of-year trends, employment within the retail industry seems to be largely flat since 2015 with little gains to be expected even with projections up until 2027. 

From our review of industries employing the greatest number of computer scientists, we know that Retail was one of largest employers, but what we can see from the data is that Retail is a seasonal and volatile industry which may not provide job stability, even for computer scientists. 
 

*Professional and Business Services*

With Professional and Business Services, we see similar overall employment numbers to Government and Health and Education, but we also see a similar swift post-pandemic recovery period similar to the Financial industry, reaching pre-pandemic employment levels mid-2021. Previous to 2020, we saw employment within the Professional and Business Services industry at almost 22,000,000 employed. By 2022, those levels were exceeded and are projected to reach almost 23,000,000 by 2024. 

In terms of seasonality, what we see is a dip in employment at the end of each calendar year which makes sense considering this industry is comprised of a lot of B2B consultants where engagements may conclude at the end of their clients’ fiscal years. However, employment has steadily increased since 2021 and is expected to continue well into 2027. 

When we look at seasonality as reflected in the "yearly" visualization, we see that mid-May, there's a spike in employment before dipping down in June, then employment trends upwards again.

*Manufacturing*

At a peak of 13,000,000 full-time employees in 2019, manufacturing employs the 2nd lowest number of FTEs from the industries we’ve reviewed, but unlike Financial Services, Manufacturing didn’t reach pre-pandemic employment levels until 2023 and is expected to increase by less than 1,000,000 jobs by 2027.

What we can observe from the visualizations is that employment has largely been flat since 2015, experiencing neither significant highs or lows, until the pandemic which took employment to the lowest levels of the period examined (2015-2027). Considering the safety requirements, new regulations, and extended time period before manufacturing employees could reliably return to work, this is to be expected. 

With regards to seasonality, when we look at the "holidays" visualization, what we see is that employment seems to spike in March and mid-May with sharp declines in the month after.

*BLS Data Analysis Conclusion*

In terms of real numbers, Health and Education has the highest number of full-time employees at more than 26,000,000 and is projected to reach 29,000,000 by 2027, outpacing all the other industries in terms of growth and real jobs. The next industry with the highest number of jobs and with a strong upward trend of growth is Professional and Business Services. Of all the industries, these are the two industries where there is a large number of jobs, job growth, and also job stability, so we would recommend that those pursuing a career in computer science should look at those industries for employment. That being said, from review of supplementary resources, we found that within the Government industry (specifically within the federal government), there is a strong desire to build and recruit an artificial intelligence workforce to secure the interests of the U.S. now and in the future. More on this topic follows in the subsequent section.

*Supplementary Source Findings*

Since we wanted to understand the realities of what was happening with regards to employment in artificial intelligence jobs, and we weren’t able to get sufficiently granular answers from the BLS data, we consulted additional sources for information and found that the need for workers in artificial intelligence within the U.S. far exceeded our expectations, particularly within the Government industry.

To start with is the simplest data point. We searched for artificial intelligence jobs on LinkedIn and found that as of January 8th, 700 jobs were currently listed within the United States. We also spoke with Tavis Lochhead, Co-founder of Kadoa, a data scraping tool which connects to various data sources, including job boards. Kadoa provides a feed for new job postings, so candidates can apply to the hottest jobs before others are aware of them. Although a paid service, Kadoa does provide a 2-week trial and may be a resource that our classmates look into using as they near completion of this bootcamp. Although 700 jobs doesn’t seem like much for a single search on a single job listing platform, it is important to note that these are corporate jobs within a growing field, and the search was only for “artificial intelligence” and did not include any additional, tangential terms (e.g. data scientist, machine learning, Python programmer, etc.). Where we found the most promising information related to AI employment was within 2 government reports, *The Impact of Artificial Intelligence on the Future of Workforces in the European Union and The United States of America* and *2021 Final Report*, published by The National Security Commission on Artificial Intelligence.

One of the areas highlighted in *The Impact of Artificial Intelligence on the Future of Workforces in the European Union and The United States of America* was the risk of workers being displaced by automation through AI versus their roles being augmented by AI. This can create further social distortion between the “haves” and the “have-nots” as jobs are eliminated, and workers are unable to be re-employed and/or reskilled into new roles. The report details very possible real-world scenarios (both which have already been demonstrated and what is expected to happen from similar world-changing technological innovations in the past): Exacerbation of social problems, particularly discrimination, security risks, and ethical concerns of how AI may impact our lives in new, uncomfortable ways. This report further details occupations where they see the greatest immediate likelihood of automation, namely: “Clinical laboratory technicians, chemical engineers, optometrists, and power plant operators” (Council of Economic Advisors, 2022). One area of note is that in our analysis, we have seen the flatness of the manufacturing industry, and this report by the CEA states that machinists are also likely to be automated by AI, further reducing employment in the Manufacturing industry. What the CAE does find as roles where AI is likely to augment rather than automate jobs is with industrial engineers and analysts. Specific to our classmates, the role of analyst may be a good entry-point into working with AI, if they don’t specifically want to be a programmer. 

With regards to overall employment, the CAE notes an interesting trend, provided by a U.S. Census Bureau study in 2019: 

> Among AI adopters, 15 percent report that AI increased overall employment levels and 6 percent indicate that AI decreased them, which points to the
>  limited and somewhat ambiguous effects of AI on employment levels. Instead, 41 percent of AI adopters increased their skill demand, while almost no
>  firms (less than 2 percent) report a reduction in their demand for skills. This self-reported increase in firms’ skill requirements when they adopt
>  AI explains part of the well-known skills gap an highlights the importance of investments in worker skills (Council of Economic Advisors, 2022).

Although initially promising, this finding was from 2019 before generative AI became such a part  of discussions in both the public and private sectors. It is likely that the organizations adopting AI earlier were ones that had specific use-cases which did not include the entirety of their organizational fabric. 

Now, if we turn our focus to The National Security Commission on Artificial Intelligence’s *2021 Final Report*, we get a much different picture. At almost 800 pages, the report is extensive, even exhaustive, but one concern was stated many times, multiple ways, and with no small degree of urgency: The United States does not have the workers skilled in AI that it needs to protect our national security, our democracy, and our economic stability. Take this quote into consideration:

>The human talent deficit is the government’s most conspicuous AI deficit and the single greatest inhibitor to buying, building, and fielding AI-enabled
> technologies for national security purposes. This is not a time to add a few new positions in national security departments and agencies for Silicon
> Valley technologists and call it a day. We need to build entirely new talent pipelines from scratch. We should establish a new Digital Service Academy
> and a civilian National Reserve to grow tech talent with the same seriousness of purpose that we grow military officers. The digital age demands a
> digital corps. Just as important, the United States needs to win the international talent competition by improving both STEM education and our system
> for admitting and retaining highly skilled immigrants (The National Security Commission on Artificial Intelligence (2021).

The report details how the U.S. needs to build in the infrastructure for AI research & development, create all new talent pipelines with new ways of working, thinking, and operating, right down to building a new academy, a “United States Digital Service Academy” which provides undergraduate and graduate degrees, receiving both government and private funding. They recommend recruiting those not typically recruited for government work, including part-time employees, using a message of “spend[ing] a career performing meaningful work focused on their field of expertise in government.” 

Coming back to our initial research into computer science jobs reported by the Bureau of Labor Statistics, the NSCAI reports, “In 2020, there were more than 430,000 open computer science jobs in the United States, while only 71,000 new computer scientists graduate from American universities each year” (The National Security Commission on Artificial Intelligence (2021).

The report provided by the NSCAI thoroughly illustrated the need for artificial intelligence professionals within the Government industry, which, although the data from BLS was not as compelling as the industries of Healthcare and Education and Professional and Business Services, we thought it was compelling enough to include it in this report as a potential future for our classmates. 

Finally, an additional resource we consulted was an article published by CNBC. In her article “The most in-demand AI job of 2023 can pay over $200,000 and offers remote opportunities”, Morgan Smith states, “Openings for generative AI jobs are up 306%” over the past year, and “the sheer volume of available AI jobs on [ZipRecruiter] is still ‘much, much greater’ than it was before the pandemic” (2023). Smith further states that the “hottest AI job on the market right now” is that of data scientist which was the most-advertised job on Indeed and second most-posted job on ZipRecruiter over the 6 months before article publication in November of last year.

Now, that we’ve learned some of what we wished to understand about employment trends in the United States which helps us think more strategically about which industries we may wish to pursue for a career in artificial intelligence, now we’d like to provide some additional learnings we’ve had over the past 2 weeks, outside of our project focus.

---

In addition to what we’ve learned about the state of U.S. employment (past, present, and future), we’ve learned quite a bit through this project, specifically about challenges involved in sourcing, accessing, understanding and using such an extensive dataset which is supported by a government agency.

**Key Learnings about Working with BLS Data**

-	Accessing and using BLS data: The upside of BLS data is that its trustworthy as a data source; however, that data may not be presented in a way that easy to understand, consume, and use, and finding supporting documentation or contacts to help is next-to-impossible.
-	Understanding BLS data: For someone who is new to BLS data, it may be cumbersome to understand, but most concepts and data points are defined; however, finding it may not be in the most user-friendly way, so you have to really look around.
-	Getting help working with BLS data: Getting help is the hardest part of using BLS data because there are no listed contacts, only a general inquiry form. We even reached out to BLS data scientists on LinkedIn, and our contact was unable to help because of confidentiality; however, he did put us in contact with some people at BLS who may be able to help.
-	Limitations of BLS data: Because AI is such a new occupation, it is not reported separately, and roles which would include artificial intelligence aspects go across 5 different NAICS codes. For this reason, we couldn’t get the type of information we were looking for and had to approach the assignment differently. 
-	Sourcing information to supplement BLS government data: To get some insight into what is happening with artificial intelligence jobs, we had to consult additional, potential data sources, articles, and publications. 

Along with our learnings about working with the BLS data, we learned quite a bit about working together as a team over the past 2 weeks and how we can apply these learnings to our subsequent project teams, both in class and professionally.

**Key Learnings about Working as a Project Team**

-	Establishing areas of ability & setting ourselves up for success: First off, we had to learn each other’s capabilities, competencies, and comfort levels by discussing the project requirements, breaking them into various deliverables, and learning who is experienced and feels confident taking on those activities and deliverables. But, we also learned strengths unique to each person from work experience in data science, to programming knowledge, to creation of presentations, project plans and descriptions, and even connecting with SMEs outside our team for questions. 

-	Pivoting and rethinking assumptions: We had more pivots over the past 2 weeks than a salsa team in a dance-off, and if you’re wondering, yes, we did put this in for anyone who may actually be reading all this documentation. But, to the point, we pivoted multiple times to ensure that we could meet the requirements of the project while still providing ourselves and the rest of the class some helpful information to consider as they look to a future career in artificial intelligence.

-	Getting outside help: Although we used the typical sources for help (Bard, ChatGPT, internet resources, Prophet documentation), we were determined to try to find answers to as many questions as we could. For this, we reached out to various SMEs which included: Personal connections, Meta data scientists who work with Prophet, BLS data scientists, and even a new product company, Kadoa, which scrapes job boards and provides listings of new jobs based on a specific query. This resulted in a conversation with a Co-Founder of Kadoa, a LinkedIn group chat with Prophet’s Data Science Manager, and a referral from a BLS data scientist to additional contacts who could help us. This helped us rethink our work and our approach and also provided contacts who can potentially lead us to job prospects in the future. 

-	Comparison to real-world scenarios: Although this project is meant to simulate some real-world working scenarios, there are key differences: First, the amount of time and effort that can be applied to this project when it’s not our full-time job is limited, and as such, scheduling time together can be difficult. This team did an incredible job of consistently checking in (which is something considering the holiday week) and finding time where we could work together, even if in smaller groups. Next, one of the group meetings we set up was a tutoring session where we expected that we could review the code together with the tutor and get help with our model, so that we all would understand the challenges, the changes needed, the explanation of why that was what was needed, and we could immediately jump into the next activities and deliverables, keeping everyone up-to-date and working synchronously. Unfortunately, the tutor told us it was against policy to have a session with more than one student, and that it was similarly against policy to substitute in the student who had the most questions for the one who set up the original appointment. This experience by no means reflects a real-world working scenario. In the real-world, when we’re on a project team and meet an obstacle, we pull everyone who can inform a solution on a call together. Thus, although this project was meant to be illustrative of a real-world working scenario, the tutoring policies inhibited that illustration and created delays we did not expect. 

-	Using project to set ourselves and one another up for career success: During our discussions together, we learned a great deal about one another, our interest in potential roles, careers, and employers, as it became clear the team was really interested in the story the BLS data had to tell. In this, we were able to not only access and analyze the data which can help us and others in our future job-hunting strategy, but it also gave us the opportunity to have discussions about potential employers which led to connecting on LinkedIn and even providing some introductions to people who are hiring. Further, although this is a first project, it becomes something which can be used, either in its current state or in some future state, as a portfolio piece and a discussion topic which any employer of any industry would likely find interesting. In this, our team members can stand apart in the interview process. 
                
  
### Section 4: Conclusion ###

In all, we have learned a lot over the past 2 weeks. We’ve learned how to access BLS data via API and how to use Prophet to analyze time-series data. We’ve learned that computer science is one of the top 2 growing occupations, and computer scientists have a median income at 2-3x the other similarly fast-growing occupations. We’ve learned that Healthcare and Education and Business and Professional Services industries employ the most people, have the strongest, healthiest, and most stable job growth, even projecting into 2027. We’ve learned that getting the answer right on the first try is not likely (and we don’t need Prophet to tell us that), but through the pivots we made, we learned more than we expected: We learned how to reach out to others, SMEs in the industry, who were willing to help us and did. We learned how to listen to one another, learn from one another, and ultimately, depend on one another to pull off a very difficult task during a short period of time. 

**And, if that isn’t the most real-world working scenario, I don’t know what is.**


                
### Section 5: Remaining Questions for Future Exploration ###

-	What are the most desirable skillsets (for programmers and non-programmers) within the field of artificial intelligence for the next 2-5 years?
-	Where are the best places to live and work in for artificial intelligence jobs, if remote work isn’t an option?
-	Will Kadoa be a good source for our classmates to review new job postings and ultimately secure a new role in artificial intelligence?
-	How might we connect with government agencies who are seeking to build a new civilian workforce, as recommended by the NSCAI?
                
### Section 6: References ###

Sources: 

Bureau of Labor Statistics. (2023, December 5). *10 major occupational groups with higher-than-average wages projected to grow faster than average.* Retrieved from https://www.bls.gov/opub/ted/2023/10-major-occupational-groups-with-higher-than-average-wages-are-projected-to-grow-faster-than-average.htm

Bureau of Labor Statistics. (2023). *Data extracted from the Bureau of Labor Statistics API.* Retrieved from https://www.bls.gov/developers/api_python.htm

Council of Economic Advisors. (2022, December 5). *The impact of artificial intelligence on the future of workforces in the European Union and the United States of America.* Retrieved from https://www.whitehouse.gov/wp-content/uploads/2022/12/TTC-EC-CEA-AI-Report-12052022-1.pdf

LinkedIn. (n.d.). *Job listings for 'artificial intelligence'.* Retrieved 2023, January 8, from https://www.linkedin.jobs.com

OpenAI. (2023). Assistance in documenting code and providing citation guidelines [Personal communication].

The National Security Commission on Artificial Intelligence. (2021, October 5). *2021 Final Report.* Retrieved from https://cybercemetery.unt.edu/nscai/20211005220409/https://reports.nscai.gov/final-report/table-of-contents/

Smith, M. (2023, November 2). *The most in-demand AI job of 2023 can pay over $200,000 and offers remote opportunities.* CNBC.com. Retrieved from https://www.cnbc.com/2023/11/02/the-most-in-demand-ai-job-of-2023-can-pay-over-200000-and-offers-remote-opportunities.html


---

### Section 7. Code Documentation ###

Project team note: Documentation provided with assistance of ChatGPT which is cited in our References section of this README file.

### Importing Libraries & Using BLS API ###

The provided Python code is meant to interact with the Bureau of Labor Statistics (BLS) public API to retrieve data for a specific time series related to employment. It imports necessary libraries, sets API parameters, sends a POST request to the BLS API, processes the response, and presents the data in a Pandas DataFrame.

**Code Walkthrough**

*Importing Libraries*

    import requests
    import json
    import pandas as pd

The code begins by importing three essential libraries: requests, json, and pandas. These libraries are required for making HTTP requests, working with JSON data, and handling data in tabular form, respectively.

*Defining API Parameters*

      api_url = “https://api.bls.gov/publicAPI/v2/timeseries/data/”
      api_key = “Your API Key here”  # Replace with your API key
      series_id = “CEU3000000001”
      start_year = “2015”
      end_year = “2024”

Here, we define various parameters needed for the BLS API request:

    api_url: The API endpoint for BLS data retrieval.
    Api_key: Your unique API key (You should replace “Your API Key here” with your actual API key).
    Series_id: The unique identifier for the specific time series data (employment data in this case).
    Start_year: The starting year for the data query.
    End_year: The ending year for the data query.

*Formatting the Request Body*

    data = json.dumps({
        "seriesid": [series_id],
        "startyear": start_year,
        "endyear": end_year,
        "registrationkey": api_key
    })

In this section, the code creates a JSON-formatted request body. It includes the seriesid, startyear, endyear, and registration key as required by the BLS API. The values are taken from the previously defined variables.

*Sending the POST Request*

    response = requests.post(api_url, data=data, headers={"Content-type": "application/json"})
    response_data = response.json()

This code segment sends a POST request to the BLS API using the requests.post method. The request body (data) and headers are set accordingly. The API response is then converted from JSON format to a Python dictionary and stored in the response_data variable.

*Checking Request Status*

    if response_data["status"] == "REQUEST_SUCCEEDED":
        print("Request succeeded")
    else:
        print("Request failed")

Here, the code checks the status of the API request. If the request is successful (status is "REQUEST_SUCCEEDED"), it prints "Request succeeded." Otherwise, it prints "Request failed."

*Extracting and Formatting Data*

    series_data = response_data["Results"]["series"][0]["data"]

    df = pd.DataFrame(series_data)
    df = df.rename(columns={"year": "Year", "period": "Month", "value": "Value", "footnotes": "Footnotes"})
    df = df.reset_index(drop=True)

This section of the code extracts the actual data from the API response, which is nested within the JSON structure. It then converts the data into a Pandas DataFrame for easy manipulation. Column names are also renamed for clarity, and the index is reset.
    
*Importing the os Library*

    import os

The code begins by importing the os library. This library is essential for interacting with the operating system, including functions related to file and directory operations.

*Printing the Current Working Directory*

    print(os.getcwd())

This line of code utilizes the os.getcwd() function to retrieve and print the current working directory (CWD). The CWD is the directory in which the Python script is executed.

*Saving Data to a CSV File*

    df.to_csv('data.csv', index=False)

In this section, the code uses the Pandas DataFrame df to save its contents to a CSV (Comma-Separated Values) file named "data.csv." The to_csv method is called on the DataFrame, and two parameters are specified:

'data.csv': The name of the CSV file where the data will be saved.
index=False: This parameter instructs Pandas not to include the index column in the CSV file.

*Displaying the First Rows of the DataFrame*

    df.head()

Finally, the code uses the head() method to display the first few rows of the DataFrame df. This is a convenient way to quickly inspect the data to ensure it has been loaded and processed correctly.

*Adding the Covid "Holiday"*

Creating a DataFrame with specific data:

    covid = pd.DataFrame({
      'holiday': 'covid',
      'ds': pd.date_range(start='2020-04-01', end='2020-05-01', freq='D'),
    })

This part of the code creates a pandas DataFrame named covid. A DataFrame is a two-dimensional, size-mutable, and potentially heterogeneous tabular data structure with labeled axes (rows and columns).

*Dictionary to define the DataFrame*

The DataFrame is created from a dictionary with two keys: 'holiday' and 'ds'.

'holiday' Key:
For the key 'holiday', the value is set to the string 'covid'. This implies that each row in the DataFrame under the 'holiday' column will have the value 'covid'.

'ds' Key:
The value associated with the key 'ds' is created using the pd.date_range function. This function generates a sequence of dates.

start='2020-04-01': This sets the start of the date range to April 1, 2020.
end='2020-05-01': This sets the end of the date range to May 1, 2020.
freq='D': This sets the frequency of the date range to 'D', which stands for 'daily'. This means a new date will be generated for each day within the specified range.
The resulting DataFrame, covid, will have two columns: 'holiday' and 'ds'. The 'holiday' column will contain the string 'covid' for each row, and the 'ds' column will contain dates starting from April 1, 2020, to May 1, 2020, with one date per row.

### Government Industry ###

*Reading an Excel File*

    df = pd.read_excel('government.xlsx')

In this section, the code uses the pd.read_excel() function to read the contents of an Excel file named "government.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

    df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Code Overview*

The Python code snippet below performs several tasks related to time series forecasting using the Prophet library:

-	Imports the required libraries, including Prophet, and matplotlib for plotting.
-	Renames columns in the DataFrame to match Prophet's expected format.
-	Prepares the data for modeling.
-	Creates a Prophet model and adds seasonality.
-	Fits the model to the data.
-	Generates a future dataframe for forecasting.
-	Makes a forecast using the trained model.
-	Visualizes the forecast and its components using matplotlib.

*Importing Libraries*

    import prophet
    from prophet.plot import plot_components
    import matplotlib.pyplot as plt

The code starts by importing the necessary libraries, including Prophet for time series forecasting, and matplotlib for visualization.

*Renaming Columns*

    df = df.rename(columns={'Date': 'ds'})
    df['y'] = df['Value']

This section renames the columns in the Pandas DataFrame df to match the expected input format of Prophet. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values.

*Creating a Prophet Model*

    m = prophet.Prophet(interval_width=0.9)
    m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. We chose 0.9 because we were more comfortable with that level of certain (as opposed to a higher value). Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This captures monthly seasonality in the data.

*Fitting the Model*

    m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data.

*Generating a Future Dataframe*

    future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data.

*Making a Forecast*

    forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

    fig1 = m.plot(forecast)
    plt.show()

    fig2 = plot_components(m, forecast)
    plt.show()

Two plots are generated to visualize the forecast and its components. fig1 displays the overall forecast, including the observed data, predicted values, and uncertainty intervals. fig2 shows the individual components of the forecast, such as trend and seasonality. Both plots are displayed using matplotlib's plt.show() function.

### Health and Education Industries ###

*Reading Data from Excel*

    df = pd.read_excel('health_education.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "health_education.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

    df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Renaming Columns*

    df = df.rename(columns={'Date': 'ds'})
    df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

    m = prophet.Prophet(interval_width=0.9)
    m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

    m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

    future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

    forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

    fig1 = m.plot(forecast)
    plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

    fig2 = plot_components(m, forecast)
    plt.show()


Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

### Financial Activities Industry ###
*Reading Data from Excel*

    df = pd.read_excel('financial_activities.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "financial_activities.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

    df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Code Overview*
The Python code provided below follows a similar structure to the previous sections. It focuses on creating a time series forecast using the Prophet library. Specifically, it reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and finally visualizes the forecast and its components.

*Code Walkthrough*

*Renaming Columns*

    df = df.rename(columns={'Date': 'ds'})
    df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

    m = prophet.Prophet(interval_width=0.9)
    m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

    m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

    future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

    forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

    fig1 = m.plot(forecast)
    plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

    fig2 = plot_components(m, forecast)
    plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

### Professional and Business Services Industries ###

*Code Overview*
The Python code provided below continues the process of reading data from an Excel file named "professional_business_services.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet follows a similar structure to the previous sections, focusing on data loading and initial inspection.

*Code Walkthrough*

*Reading Data from Excel*

    df = pd.read_excel('professional_business_services.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "professional_business_services.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

    df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

*Code Overview*
The following Python code continues the process of creating a time series forecast using the Prophet library. It reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and visualizes the forecast and its components. This code is consistent with the parameters used in the previous sections.

*Code Walkthrough*

*Renaming Columns*

    df = df.rename(columns={'Date': 'ds'})
    df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

    m = prophet.Prophet(interval_width=0.9)
    m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

    m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

    future = m.make_future_dataframe(freq='M', periods=36)

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

    forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

    fig1 = m.plot(forecast)
    plt.show()

In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

    fig2 = plot_components(m, forecast)
    plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.

### Manufacturing ###

*Code Overview*

The provided Python code continues the process of reading data from an Excel file named "manufacturing.xlsx" into a Pandas DataFrame and displaying the first few rows of the DataFrame. This code snippet is consistent with the previous sections, focusing on data loading and initial inspection.

*Code Walkthrough*

*Reading Data from Excel*

    df = pd.read_excel('manufacturing.xlsx')

In this section, the code uses the Pandas read_excel() function to read the contents of an Excel file named "manufacturing.xlsx." The data from the Excel file is loaded into a Pandas DataFrame named df. This operation allows for easy access and manipulation of the data within Python.

*Displaying the First Rows of the DataFrame*

    df.head()

Finally, the code uses the head() method on the Pandas DataFrame df to display the first few rows of the loaded data. This provides a quick preview of the data's structure and content, making it easier to verify that the data has been read correctly.

The following Python code continues the process of creating a time series forecast using the Prophet library. It reads the data from the Pandas DataFrame df, prepares it for modeling with Prophet, fits a Prophet model to the data, generates a future dataframe for forecasting, makes a forecast using the trained model, and finally visualizes the forecast and its components. This code is consistent with the parameters used in the previous sections.

*Code Walkthrough*

*Renaming Columns*

    df = df.rename(columns={'Date': 'ds'})
    df['y'] = df['Value']

This section of the code renames the columns in the Pandas DataFrame df to match the expected input format of the Prophet library. The "Date" column is renamed to "ds," and the "Value" column is renamed to "y." This step is crucial for Prophet to recognize the date and target values correctly.

*Creating a Prophet Model*

    m = prophet.Prophet(interval_width=0.9)
    m.add_seasonality(name='monthly', period=30.5, fourier_order=1)

Here, a Prophet model named m is created with an optional interval_width parameter set to 0.9, which defines the uncertainty interval for the forecast. Additionally, a monthly seasonality component is added to the model with a period of approximately 30.5 days and a Fourier order of 1. This allows Prophet to capture monthly seasonality patterns in the data.

*Fitting the Model*

    m.fit(df)

The code fits the Prophet model m to the prepared DataFrame df. This step estimates the model parameters and captures the underlying patterns in the data, including trend and seasonality.

*Generating a Future Dataframe*

A future dataframe named future is created, which includes timestamps for future dates. In this case, it is set to include monthly timestamps for 36 periods (months) beyond the last date in the original data. This allows for forecasting beyond the current data.

*Making a Forecast*

    forecast = m.predict(future)

The code generates a forecast using the trained Prophet model m for the dates in the future dataframe. The forecast includes predicted values, uncertainty intervals, and other information.

*Visualizing the Forecast*

    fig1 = m.plot(forecast)
    plt.show()


In this section, the code generates a plot (fig1) to visualize the forecasted values, including the observed data, predicted values, and uncertainty intervals. The plot is displayed using matplotlib's plt.show() function.

*Visualizing the Components of the Forecast*

    fig2 = plot_components(m, forecast)
    plt.show()

Another plot (fig2) is created to visualize the individual components of the forecast, such as trend and seasonality. This provides insights into the underlying patterns that contribute to the forecast. The plot is displayed using matplotlib's plt.show() function.


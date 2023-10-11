This project is a simple, yet comprehensive, job scraping library.

### Installation

```
pip install python-jobspy
```

_Python version >= [3.10](https://www.python.org/downloads/release/python-3100/) required_

### Usage

```python
from jobspy import scrape_jobs

jobs = scrape_jobs(
    site_name=["indeed", "linkedin", "zip_recruiter"],
    search_term="software engineer",
    location="Dallas, TX",
    results_wanted=10,
    country_indeed='USA'  # only needed for indeed
)
print(f"Found {len(jobs)} jobs")
print(jobs.head())
jobs.to_csv("jobs.csv", index=False)

# output to Excel
# jobs.to_xlsx('jobs.xlsx', index=False)

```

### Output

```
SITE           TITLE                             COMPANY_NAME      CITY          STATE  JOB_TYPE  INTERVAL  MIN_AMOUNT  MAX_AMOUNT  JOB_URL                                            DESCRIPTION
indeed         Software Engineer                 AMERICAN SYSTEMS  Arlington     VA     None      yearly    200000      150000      https://www.indeed.com/viewjob?jk=5e409e577046...  THIS POSITION COMES WITH A 10K SIGNING BONUS!...
indeed         Senior Software Engineer          TherapyNotes.com  Philadelphia  PA     fulltime  yearly    135000      110000      https://www.indeed.com/viewjob?jk=da39574a40cb...  About Us TherapyNotes is the national leader i...
linkedin       Software Engineer - Early Career  Lockheed Martin   Sunnyvale     CA     fulltime  yearly    None        None        https://www.linkedin.com/jobs/view/3693012711      Description:By bringing together people that u...
linkedin       Full-Stack Software Engineer      Rain              New York      NY     fulltime  yearly    None        None        https://www.linkedin.com/jobs/view/3696158877      Rain’s mission is to create the fastest and ea...
zip_recruiter Software Engineer - New Grad       ZipRecruiter      Santa Monica  CA     fulltime  yearly    130000      150000      https://www.ziprecruiter.com/jobs/ziprecruiter...  We offer a hybrid work environment. Most US-ba...
zip_recruiter Software Developer                 TEKsystems        Phoenix       AZ     fulltime  hourly    65          75          https://www.ziprecruiter.com/jobs/teksystems-0...  Top Skills' Details• 6 years of Java developme...
```

### Parameters for `scrape_jobs()`

```plaintext
Required
├── site_type (List[enum]): linkedin, zip_recruiter, indeed
└── search_term (str)
Optional
├── location (int)
├── distance (int): in miles
├── job_type (enum): fulltime, parttime, internship, contract
├── proxy (str): in format 'http://user:pass@host:port' or [https, socks]
├── is_remote (bool)
├── results_wanted (int): number of job results to retrieve for each site specified in 'site_type'
├── easy_apply (bool): filters for jobs that are hosted on LinkedIn
├── country_indeed (enum): filters the country on Indeed (see below for correct spelling)
├── offset (num): starts the search from an offset (e.g. 25 will start the search from the 25th result)
```

### JobPost Schema

```plaintext
JobPost
├── title (str)
├── company (str)
├── job_url (str)
├── location (object)
│   ├── country (str)
│   ├── city (str)
│   ├── state (str)
├── description (str)
├── job_type (enum): fulltime, parttime, internship, contract
├── compensation (object)
│   ├── interval (enum): yearly, monthly, weekly, daily, hourly
│   ├── min_amount (int)
│   ├── max_amount (int)
│   └── currency (enum)
└── date_posted (date)
└── emails (str)
└── num_urgent_words (int)
└── is_remote (bool) - just for Indeed at the momen
```

### Exceptions

The following exceptions may be raised when using JobSpy:

* `LinkedInException`
* `IndeedException`
* `ZipRecruiterException`

## Supported Countries for Job Searching

### **LinkedIn**

LinkedIn searches globally & uses only the `location` parameter.

### **ZipRecruiter**

ZipRecruiter searches for jobs in **US/Canada** & uses only the `location` parameter.

### **Indeed**

Indeed supports most countries, but the `country_indeed` parameter is required. Additionally, use the `location`
parameter to narrow down the location, e.g. city & state if necessary.

You can specify the following countries when searching on Indeed (use the exact name):

|                      |              |            |                |
|----------------------|--------------|------------|----------------|
| Argentina            | Australia    | Austria    | Bahrain        |
| Belgium              | Brazil       | Canada     | Chile          |
| China                | Colombia     | Costa Rica | Czech Republic |
| Denmark              | Ecuador      | Egypt      | Finland        |
| France               | Germany      | Greece     | Hong Kong      |
| Hungary              | India        | Indonesia  | Ireland        |
| Israel               | Italy        | Japan      | Kuwait         |
| Luxembourg           | Malaysia     | Mexico     | Morocco        |
| Netherlands          | New Zealand  | Nigeria    | Norway         |
| Oman                 | Pakistan     | Panama     | Peru           |
| Philippines          | Poland       | Portugal   | Qatar          |
| Romania              | Saudi Arabia | Singapore  | South Africa   |
| South Korea          | Spain        | Sweden     | Switzerland    |
| Taiwan               | Thailand     | Turkey     | Ukraine        |
| United Arab Emirates | UK           | USA        | Uruguay        |
| Venezuela            | Vietnam      |            |                |


  

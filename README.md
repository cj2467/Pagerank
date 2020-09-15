# Pagerank - Implementing the Original Google algorithm

This repo contains the code for a rudimentary search engine for the website of the Law Fare Blog (https://www.lawfareblog.com). Built as practive for a Data Mining class. The pagerank.py document contains the brains of the search calculations written in python. The lawfareblog.csv.gz and small.csv.gz files contain the website backlinks and act as the data for this project.

## Part 1 - Pagerank

Results to the command `pagerank.py --data=./small.csv.gz --verbose` gives the basic ranking of urls to the site:

```
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=6.3850e+00 url=4
INFO:root:rank=1 pagerank=4.8028e+00 url=6
INFO:root:rank=2 pagerank=3.2527e+00 url=5
INFO:root:rank=3 pagerank=1.8036e-01 url=2
INFO:root:rank=4 pagerank=1.2882e-01 url=3
INFO:root:rank=5 pagerank=1.1278e-01 url=1
```


Results to the command `pagerank.py --data=./lawfareblog.csv.gz --search_query='corona'` applies the pagerank to the single term "corona":
```
DEBUG:root:computing indices
DEBUG:root:computing values
tensor(16862.)
INFO:root:rank=0 pagerank=4.6220e-03 url=www.lawfareblog.com/lawfare-podcast-united-nations-and-coronavirus-crisis
INFO:root:rank=1 pagerank=4.0801e-03 url=www.lawfareblog.com/house-oversight-committee-holds-day-two-hearing-government-coronavirus-response
INFO:root:rank=2 pagerank=2.6277e-03 url=www.lawfareblog.com/britains-coronavirus-response
INFO:root:rank=3 pagerank=2.5545e-03 url=www.lawfareblog.com/prosecuting-purposeful-coronavirus-exposure-terrorism
INFO:root:rank=4 pagerank=2.3685e-03 url=www.lawfareblog.com/israeli-emergency-regulations-location-tracking-coronavirus-carriers
INFO:root:rank=5 pagerank=2.3016e-03 url=www.lawfareblog.com/why-congress-conducting-business-usual-face-coronavirus
INFO:root:rank=6 pagerank=2.2905e-03 url=www.lawfareblog.com/livestream-house-oversight-committee-holds-hearing-government-coronavirus-response
INFO:root:rank=7 pagerank=2.2640e-03 url=www.lawfareblog.com/congressional-homeland-security-committees-seek-ways-support-state-federal-responses-coronavirus
INFO:root:rank=8 pagerank=2.1999e-03 url=www.lawfareblog.com/paper-hearing-experts-debate-digital-contact-tracing-and-coronavirus-privacy-concerns
INFO:root:rank=9 pagerank=2.0459e-03 url=www.lawfareblog.com/cyberlaw-podcast-how-israel-fighting-coronavirus
```

Results to the command `pagerank.py --data=./lawfareblog.csv.gz` show the top ten related pages to the homepage:
```
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=8.7955e+00 url=www.lawfareblog.com/litigation-documents-related-appointment-matthew-whitaker-acting-attorney-general
INFO:root:rank=1 pagerank=8.7955e+00 url=www.lawfareblog.com/lawfare-job-board
INFO:root:rank=2 pagerank=8.7955e+00 url=www.lawfareblog.com/masthead
INFO:root:rank=3 pagerank=8.7955e+00 url=www.lawfareblog.com/litigation-documents-resources-related-travel-ban
INFO:root:rank=4 pagerank=8.7955e+00 url=www.lawfareblog.com/subscribe-lawfare
INFO:root:rank=5 pagerank=8.7955e+00 url=www.lawfareblog.com/documents-related-mueller-investigation
INFO:root:rank=6 pagerank=8.7955e+00 url=www.lawfareblog.com/topics
INFO:root:rank=7 pagerank=8.7955e+00 url=www.lawfareblog.com/our-comments-policy
INFO:root:rank=8 pagerank=8.7955e+00 url=www.lawfareblog.com/upcoming-events
INFO:root:rank=9 pagerank=8.7955e+00 url=www.lawfareblog.com/about-lawfare-brief-history-term-and-site
```

Results to the command `pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2` show the top ten related pages to the homepage, but this time removes spam with a filter rate of .2:

```
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.7606e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=3.1803e+00 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=3.1615e+00 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=1.9800e+00 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=4 pagerank=1.8494e+00 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
INFO:root:rank=5 pagerank=1.8429e+00 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=6 pagerank=1.8422e+00 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=7 pagerank=1.8356e+00 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=8 pagerank=1.7335e+00 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=9 pagerank=9.5979e-01 url=www.lawfareblog.com/events
```


## Part 2 - The personalization vector
Results to the command `pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'` show the top ten related pages to the homepage, but this time using the personalization vector:

```
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=1.5925e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=8.3592e-01 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=2 pagerank=8.1987e-01 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=3 pagerank=8.1986e-01 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=4 pagerank=8.1982e-01 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=5 pagerank=8.1790e-01 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=6 pagerank=8.1788e-01 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=7 pagerank=7.8217e-01 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=8 pagerank=7.3029e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=9 pagerank=7.3008e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
```


## Part 3 - Experimentation

I am currious to see how much this particular site is covering this election, and elections in general.
For General Election coverage I can use the command `pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --search_query='-election'` show the top ten related pages:

`DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=4.7606e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=3.1803e+00 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=2 pagerank=3.1615e+00 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=3 pagerank=1.9800e+00 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=4 pagerank=1.8494e+00 url=www.lawfareblog.com/summary-david-holmess-deposition-testimony
INFO:root:rank=5 pagerank=1.8429e+00 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=6 pagerank=1.8422e+00 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=7 pagerank=1.8356e+00 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=8 pagerank=1.7335e+00 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=9 pagerank=9.5979e-01 url=www.lawfareblog.com/events`

Now the same thing but with the personalization vector `pagerank.py --data=./lawfareblog.csv.gz --filter_ratio=0.2 --personalization_vector_query='corona' --search_query='-corona'`:

```
DEBUG:root:computing indices
DEBUG:root:computing values
INFO:root:rank=0 pagerank=1.5925e+00 url=www.lawfareblog.com/trump-asks-supreme-court-stay-congressional-subpeona-tax-returns
INFO:root:rank=1 pagerank=8.3592e-01 url=www.lawfareblog.com/senate-examines-threats-homeland
INFO:root:rank=2 pagerank=8.1987e-01 url=www.lawfareblog.com/what-make-first-day-impeachment-hearings
INFO:root:rank=3 pagerank=8.1986e-01 url=www.lawfareblog.com/livestream-house-armed-services-committee-hearing-f-35-program
INFO:root:rank=4 pagerank=8.1982e-01 url=www.lawfareblog.com/whats-house-resolution-impeachment
INFO:root:rank=5 pagerank=8.1790e-01 url=www.lawfareblog.com/livestream-nov-21-impeachment-hearings-0
INFO:root:rank=6 pagerank=8.1788e-01 url=www.lawfareblog.com/opening-statement-david-holmes
INFO:root:rank=7 pagerank=7.8217e-01 url=www.lawfareblog.com/congress-us-policy-toward-syria-and-turkey-overview-recent-hearings
INFO:root:rank=8 pagerank=7.3029e-01 url=www.lawfareblog.com/covid-19-speech-and-surveillance-response
INFO:root:rank=9 pagerank=7.3008e-01 url=www.lawfareblog.com/lawfare-live-covid-19-speech-and-surveillance
```

Seeing as the results are mostly about the US election in 2020, I do not need to search again.

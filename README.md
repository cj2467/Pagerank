# Pagerank - Implementing the Original Google algorithm

This repo contains the code for a rudimentary search engine for the website of the Law Fare Blog (https://www.lawfareblog.com). Built as practive for a Data Mining class. The pagerank.py document contains the brains of the search calculations written in python. The lawfareblog.csv.gz and small.csv.gz files contain the website backlinks and act as the data for this project.

## Part 1

Results to the command 'pagerank.py --data=./small.csv.gz --verbose':

'DEBUG:root:computing indices
DEBUG:root:computing values
tensor(6.)
INFO:root:rank=0 pagerank=6.3850e+00 url=4
INFO:root:rank=1 pagerank=4.8028e+00 url=6
INFO:root:rank=2 pagerank=3.2527e+00 url=5
INFO:root:rank=3 pagerank=1.8036e-01 url=2
INFO:root:rank=4 pagerank=1.2882e-01 url=3
INFO:root:rank=5 pagerank=1.1278e-01 url=1'


Results to the command 'pagerank.py --data=./lawfareblog.csv.gz --search_query='corona'':

'DEBUG:root:computing indices
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
INFO:root:rank=9 pagerank=2.0459e-03 url=www.lawfareblog.com/cyberlaw-podcast-how-israel-fighting-coronavirus'



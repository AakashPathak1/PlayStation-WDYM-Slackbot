# Unfurl Those Acronyms!

Welcome to the `Unfurl Those Acronyms Hackathon` project (SF24)  
> Team Members: Bruno Parrinello, Aakash Pathak, Arnav Rastogi, Gary Zheng, Selina Liu, Junyi Yao, Sindhu Ajoy, Yuliya Sidis, Maureen McGrath

The code for this project cannot be publicly shared, but let me know if you'd like to take a look!
 
## Background

As most of us are interns, we've had to deal with a lot of **confusing acronyms** during our time here, particularly during our onboarding week. Although acronym glossaries exist on Confluence, there are multiple glossaries that make it hard to navigate through and find the acronym we're looking for. Moreover, searching for multiple definitions for the same acronym becomes difficult. We decided to create a Slack App Integration that does this difficult work for us, and when queried with an acronym, finds all possible suggestions for that acronym across multiple Confluence glossaries! It even displays acronyms depending on the requesting user's disclosure level, to ensure that everything is on a need-to-know basis!

## Technical Overivew

### How do we fetch all this data?  
* We have a list of 1000 acronyms over 5 Confluence pages, and we use the `Confluence API` to fetch information and populate our database
* We also fetched information from Confluence pages containing employees' Email and associated Disclosure Level

### How do we know the user's disclosure level?  
* Based on the `Slack API`, we query a Confluence page that contains a list of all `C0` users for example, and verify that the user has access to the given search acronym

### Where is all this information stored?
* For security reasons, this data is stored in a `mySQL` database in a `Docker` container stored locally on the user's computer

### How do we account for typos when searching for acronyms?
* All our data is "sanitized" before storing in our database. This means that the acronym `"POC"`, `"PoC"`, `"P O C"`, `"P-o-C"` will all return the same query!

### How do we ensure our data is up to date?
* Our database is updated every day at midnight, and all our database is automatically updated with every new addition or deletion made to every `Confluence` glossary page

## Screenshots!

<img width="485" alt="Screenshot 2023-07-13 at 3 46 35 PM" src="https://github.com/AakashPathak1/PlayStationUTA-HackathonProject/assets/54967572/8773a32f-6eff-4152-8cd5-87bd78a4cb39">
<br>
<img width="193" alt="Screenshot 2023-07-13 at 3 46 49 PM" src="https://github.com/AakashPathak1/PlayStationUTA-HackathonProject/assets/54967572/fa97681c-008f-4f6f-8fb4-5298914f17be">
<br>
<img width="686" alt="Screenshot 2023-07-13 at 3 47 00 PM" src="https://github.com/AakashPathak1/PlayStationUTA-HackathonProject/assets/54967572/c8e274f8-c1aa-43f9-a5ef-e195506c3ad0">



## Setup
- `pip3 install requests`
- `pip3 install re`
- `pip3 install beautifulsoup4`
- `pip3 install mysql-connector-python`
- `pip3 install schedule`
- download docker desktop, then run `docker-compose up -d` then check in docker desktop to see the container is running
- `python3 parseUserList.py`
- `python3 ingestion.py` to fetch data and update database

### To examine data in mysql container

- `docker exec -it <docker-id> /bin/bash`
- `mysql -uroot -hlocalhost -p`, password is `example`
- `USE glossary;`
- custom query, ex. `SELECT * FROM terms;`

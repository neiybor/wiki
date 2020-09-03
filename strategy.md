<!-- TITLE: Strategy -->
<!-- SUBTITLE: Overview of Strategy at Neighbor, including Analytics, SEO & Monetization -->


# Analytics
## Data Glossary

*--Work in Progress--*

**User Type:** Domo-defined term based on how the user initially defined their use case during registration and by actions the user took. Options include: Renter, Host, Hybrid, None. For example, if a self-defined Renter creates a listing then they will also be flagged as a Host, resulting in a Hybrid user type within Domo.

**Business Type:** Neighbor-defined term based on whether the user is renting out space whose primary purpose is not storage (P2P) or if the space's primary purpose is to generate revenue through storage (Enterprise). Options include: P2P, Enterprise. *Note: May consider spliting out P2P into P2P Commercial and P2P Residential.*

**Market:** Neighbor-defined geographic areas constrained by latitude & longitude coordinates. Not stored in the database and only accessible by Master datasets (see "Master datasets" inside Domo Best Practices) or by SQL query.


## Domo Best Practices
### Creating Cards

* **Quick Filters:** Add potential filters to a card and toggle the "Quick Filter" on to allow for end-users to easily toggle between common filters (e.g., Market, Business Type, Listing Status). To join your dataset with existing Neighbor database data, see the "Master datasets" bullet of the "Managing Data" section.

### Managing Data

* **Dataset tags:** Rather than naming a dataset with your department name or data source, use a tag (e.g., Growth, KM)
* **Google Sheets:** When creating a new dataset from a Google Sheet, put a shareable link to the sheet in the dataset description to make it easy to find the actual sheet within Google Drive.
* **Master datasets:** To join new datasets with database data, use a "Master" dataset to connect with existing ETL pipelines. This allows for easier maintenance and 
global consistency. Depending on what data you are looking to join, join with the Master Reservations (all reservations plus relevant data), Master Listings (all listings plus relevant data) or Master Users (all users plus relevant data).
* **New datasources and large datasets:** Domo pricing is dependent on user seats, unique datasources and rows of data. Before connecting a datasource to Domo that Domo isn't already using, talk to Colton about Neighbor's data connectors. When pulling in a large number of rows of data, try to aggregate it before pulling into Domo to limit the number of data rows that Domo handles.


## Resources
### Neighbor Internal Research

This shared folder serves as a company-wide repository for internal research, allowing all teams to store and access the insights of other teams. When adding files, please add a descriptive title and include in the title or document who conducted the research.

https://drive.google.com/drive/folders/1whr8ET0c55MrvNK5MAtQLC9vREV9eJYv?usp=sharing

### Market Research

This shared folder contains industry reports on the self storage industry and research into other marketplace or storage companies. Feel free to add relevant files to the main folder or the Industry Reports subfolder.

https://drive.google.com/drive/folders/1g6kESdLmhGOwyfXxWu8zszEGAgCI2i8P?usp=sharing



### 2018-2020 Self-Storage Almanac Credentials

Login: https://view.imirus.com/301/signin
Username: colton@neighbor.com
Password: TKErxOGe

### Reservation Statuses
[Reservation Statuses Diagram](https://drive.google.com/file/d/1-EisaEV1Pkegq4FGR7h85ajUGN7aHubc/view?usp=sharing)

### Market Boundaries
[Market Boundaries Google Map](https://www.google.com/maps/d/u/0/edit?mid=1dHU93CiFk9Uku4xBwktYksX9vvl8n5GI&ll=34.98466619418738%2C-98.06705532567729&z=6)

# SEO
## Q4 2019 Goals
Vision: By the end of Q4 2019, regarding Neighbor SEO:
* We will make significant progress regarding page speed and crawler readability as damaging factors to our Local Landing Pages Google site rankings
* We will have tested various ways to teach Google that we are relevant for all “self storage” queries
* We will have released the best-in-industry self-storage industry data page and have begun work on state-specific self-storage industry data pages

**1. 100k organic clicks in Q4**
	A. Oct: x (+13%)
	B. Nov: x (+20%)
	C. Dec: x (+25%)
**2. 148 organic reservations in Q4**
	A. Oct: 40 (+13%)
	B. Nov: 48 (+20%)
	C. Dec: 60 (+25%)
**3. <5 seconds DLP page load speed** (3G Mobile Nexus 5)
**4. 3 A/B Tests released to increase relevance**
**5. 4 blog articles published** (including Self Storage Industry Data article)

Details - https://docs.google.com/document/d/1tqwx4QG0SMv3fcWsfUhQkE7NUAhLY6omfYaN-xiXCmI/edit?usp=sharing

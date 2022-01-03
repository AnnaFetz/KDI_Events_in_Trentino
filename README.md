## Events in Trentino 
### Knowledge and Data Integration Course 
### Academic year 2021/2022, MSc Data Science, University of Trento

----
### Material 
Link to [Official course repo](https://github.com/AnnaFetz/KDI_Events_in_Trentino)<br>
Link to [Project personal repo](https://github.com/LuciaHrovatin/KDI_project/tree/main)

### Project's Description

Project's scope intersects the **Event** domain with the **University Student Life**. 

Due to the placement of University of Trento's departments, the spatial coverage includes only the municipalities of Trento and Rovereto. <br>
Temporally, the project targets the 2019-2022 timespan, which aims at detecting and modelling the changes that occurred due to the Covid-19 pandemic in event organization and participation.<br>

The final deliverable should correspond to a website acting as a collective memory of a specific administrative area. The target users are university students, who interact with the service, standing as both <i>short-term memory</i> (i.e., working memory) and <i>long-term memory</i>, specifically episodic. While the former function filters the future events by location, duration, target age, personal interests, event category (e.g., music, shows, festivals), and secondary attributes (e.g., language, price), the latter retrieves relevant information about past events. This option focuses mainly on the event's description, tags, ranking, comments, and pictures.

### Resources
#### Knowledge Resources:
- [Wordnet](https://wordnet.princeton.edu/)
- [Schema](https://schema.org)
- [DBPEDIA](https://www.dbpedia.org/)

All the other minor knowledge resources are listed in the project's [report](https://github.com/AnnaFetz/KDI_Events_in_Trentino/blob/501f29e386902e9fe49a0017f960cfb3a8b4c351/Documentation/FinalReport.pdf). 

#### Data Resources 
A separate Git repository stores the ([final datasets](https://github.com/LuciaHrovatin/KDI_project/tree/main/Formatted_Datasets)), which have been collected from the following sites:

- [Crushite](https://www.crushsite.it/it)
- [Stayhappening](https://stayhappening.com)
- [Eventbrite](https://www.eventbrite.com)
- [Tripadvisor](https://www.tripadvisor.it)
- [Esn](https://esn.it)
- [L'Universitario](https://www.luniversitario.it)
- [OpenDATA Trentino](https://dati.trentino.it)
- [Meetup](https://www.meetup.com/it-IT)
- [Openstreetmap](https://www.openstreetmap.org/#map=9/46.0025/10.9414)
- [MyMovies](https://www.mymovies.it/cinema/trento/versione-originale)

Data regarding events coming from crushsite, stayhappening, tripadvisor, dati trentino, meetup, mymovies and ESN have been saved in JSON format, and divided by E-type.
 Their keys are data and object properties contained in the respective EG Model.<br>Namely, they are shaped according to the E-type they belong to, as <b>Cultural Events</b> example below.

```markdown
{
                "has_eventID": "",
                "has_title": "",
                "has_mode": "", #online, offline or blended
                "has_link": "",
                "has_targetAge": "",
                "has_edition": "",
                "has_festivalStatus": , #bool
                "has_language": ["it-IT"],
                "has_start": "", #datetime
                "has_end": "", #datetime
                "has_recurrency": , #bool
                "has_organizer": "",
                "has_specialAnnouncements": "",
                "has_description": "",
                "has_terminated": , #bool
                "has_hashtag": [],
                "has_distance": , #bool
                "has_schedule": "", #daily, monthly, weekly
                "has_transportMode": [],
                "has_venue": , #osm_id
                "has_virtualLocation": "", #object property
                "has_superEvent": "", #object property
                "has_originalLanguage": , #bool
                "has_performer": "",
                "has_subtitles": , #bool
                "has_guidedTour": , #bool
                "has_ticket": "", #object property
                "has_Archive": "",
                "has_freeEntrance": , #bool
            }

```

### ER description

![ER model](https://github.com/AnnaFetz/KDI_Events_in_Trentino/blob/main/Teleologies/Informal%20Modeling/er.png)

The building process of the ER was intended to resemble a real query on the final service. Thus, below an explanation of the intended hierarchy.
<li> <b>Common objects</b> were mainly considered to be existence-independent as they are uniquely identified by their attributes, and do not depend on other entity. Thanks to their generic representation and vast usage, they could be used for a (future) broader DoI.</li><br> 
<li> <b>Core objects</b> represent purpose-specific entities, such as the event type, main actors (e.g., Student) or specific facilities. According to the intended output, core objects mirror the infrastructure of the filtering system of the website. Specifically, these entities should direct the initial query and skim all the events not matching preferences. For instance, if a specific place is selected, the output will list only events taking place there.</li><br>
<li> <b>Contextual objects</b> were thought of being a further specification provided by the user to obtain a narrower list of events matching all criteria. For instance, the user would use location-specific keywords when searching for a specific set of events (e.g., Concerts in Trento's Doss).</li><br>
<li>With concerns to actions, they mostly were intentionally not defined as entities. They have been integrated as either properties or bidirectional relationships between main entities (i.e., superclasses).</li><br>
	
As stated above, the ER model has been structured following the future website's filters and its focus on searching for events, as other websites already do. The main event's type (i.e., categories) identified are the following:
	
<li><b>Social Events</b>: lead to a socialization process (i.e., people forming groups) and present repeated actions, such as drinking or dancing. A prototypical example is a Happy Hour. </li><br>
<li> <b>Education Events</b>: (academic) prearranged meetings for consultation, exchange of information, or discussion. The audience might be not actively involved.</li><br>
<li> <b>Workshop</b>: umbrella term for any laboratory event that actively involves the participants and delivers a tangible result (i.e., product), or breaks new skills.</li><br>
<li> <b>Cultural Events</b>: knowing that cultural has a broad meaning, within this project, an event is defined as cultural if it is designed for entertainment and enjoyment and is related to some branch of art, culture, or local values (i.e., performing arts, musicals, photography, and literature). The definition here adopted partially resembles the DutchCulture Database structure as it is consistent with the project's purpose.</li><br>
<li><b>Tour</b>: traveling means going from one place to another. Whereas the event's types above may be represented as happening at a specific time and in a static space, a tour event involves both a movement and some personal interests. </li><br>
<li><b>Sports Events</b>: organized occasions where a sports or exercise activity is performed at a specific location in a temporal interval. Most sports events are also part of bigger meetings and competitions. They can be periodically organised, such as the Facoltiadi or a sports course (i.e., dance course). Depending on the disciplines, schedule, competitors,	and scope (e.g., tournaments, leagues, fundraising), the events may embed different descriptors.</li><br>
		
While the Covid-19 pandemic did not particularly impact the events' categories, it constraints and modifies the concept of location. Thus, three scenarios are possible:
<ol>
	<li> Offline events have a location traditionally defined as an identifiable point in the two (or
		three) dimensional space; </li><br>
	<li> Online events, meaning occasions happening only in a virtual environment hosted on video
		communication services, such as Zoom and Google Meet; </li><br>
	<li> Blended or Hybrid events offer an offline or online attendance depending on the participant's
		needs and possibilities. </li><br>
<li> <b>CreativeWork</b> gathers all human artifacts produced during an activity or employed in an event.</li><br>   
<li> To satisfy the necessity of a memory, the ER model integrates an <b>Archive</b> entity too, aiming at keeping track of events' past history.</li><br>
<li> A final remark regards the creation of the <b>ArchitecturalBarriers</b> entity that enlarges the plethora of users and increases the quality of the final service. The information delivered focuses on the event's venue (and transport) and its accessibility. Due to the lack of standardization in this field, these properties comply with the Italian legislation DM 236/89. </li><br>
Please notice that due to timing some further changes were applied. Reference ER can be found in the project's [report](https://github.com/AnnaFetz/KDI_Events_in_Trentino/blob/501f29e386902e9fe49a0017f960cfb3a8b4c351/Documentation/FinalReport.pdf).<br>
</ol><br> 

### ETG description

<li><b>Event:</b> The CQs requiring to navigate back in time through an event's collective memory (i.e., Archive) and those demanding the distance to a certain venue were not satisfied by the previous version of the ER model. While the latter has been solved via a boolean Data property distance that filters the events based on a ray of 2km from a specific venue, the former issue induced more structural changes. Hence the adjustments focused on the consistency of information and the storage costs of sub events belonging to a super event,  such as a Festival or a Fair. To simplify the model, the Object property superEvent has been introduced, allowing a one to one relationship with the main Event and guaranteeing a single storage in Archive. Moreover, to follow the trail of a collective memory, and to ease future project's expansions, the Object property post was introduced, linking to CreativeWork, and modeling the act of posting pictures and reviews. Within this framework, also the Object property EventType and the relative sub categories have undergone several modifications. Ideally, the ER event classification model should have been mirrored by the final ETG, as it perfectly satisfied the granularity required by the CQs. However, due to the fact that the majority of our reference files required pondered parsing, and several Event's leaf nodes contained boolean properties, a less detailed but more performing option has been preferred. Thus, the ETG reflects the final ER model, that merges the contextual and core event-related Etypes and keeps the six main subcategories of Event. Hence, the Event child SocialEvent displays all the Data properties contained in DanceEvent (e.g., happyHour) and in FolkEvent. Lastly, instead of keeping one Entity per event mode (namely, offline, online, and blended), new attribute eventMode was introduced. The values allowed should identify (as string) the three event statuses: online, offline, hybrid. This simplification skims some relationships between event and location, and retains the most relevant information.</li><br>
  
<li> <b>Facility: </b>A trade off was faced: on the one hand, facilities could be categorized in sub classes, such as FoodEstablishment or Accommodation, keeping a high level of detail. On the other hand, this structure was not feasible due to the time required in data preparation and management. Therefore, all boolean Data properties of the sub-classes have been merged within <i>facilityType</i> property. Additionally, considering the CQs' requirement of listing specific food (e.g., typicalFood) or activity (e.g., hiking), the contextual attributes have been kept in separate Data properties. Hence, Facility presents properties such as cuisine and hiking. This latter example also solved the issue regarding the erasure of Landscape, that was requiring a granularity out of project's scope. </li><br>

<li> <b>Ranking: </b>In Ranking, the isDistant property was discarded in light of what discussed for Event and data availability. Thus, instead of keeping both dichotomies distance ranking and enjoyment ranking, only the latter has been kept. Moreover, the ER model was lacking the connection between the concept of ranking and the criterion followed, namely the reviews. To fill this gap, the Object property review was introduced in Ranking and linked to Review, a contextual and independent entity.</li><br>
            
<li><b>Archive: </b>Due to the concept of collective memory pursued by the Purpose, some changes were applied on the Etype Archive as it was missing some information. Thus, the hyperlinks created by hashtags, the importDate and the visualReferences were added as Data properties.</li><br>

<li><b>CreativeWork: </b> The changes regarding Review addressed a further issue: several children of CreativeWork were sharing properties and the available data would not have reached such granularity. Thus, all the common properties of CreativeWork's children have been collapsed and the children (i.e., Image, Show, Recipe, Track and Map) discarded. The super entity CreativeWork is therefore defined as a ”manifestation of creative effort including fine artwork (sculpture, paintings, drawing, sketching, performance art), dance, writing (literature) film-making, and composition". </li><br>

### Final Links 

<li> FINAL ETG : https://github.com/AnnaFetz/KDI_Events_in_Trentino/tree/main/Teleologies/Formal%20Modeling </li>
<li> FINAL KG : https://github.com/AnnaFetz/KDI_Events_in_Trentino/tree/main/Datasets/Data%20Integration </li>

<b>NOTE:</b> please note that the final KG is split between Entities RDF Files, due to some last-minute changes. <br>

### Support or Contact
Please send an email to [Anna Fetz](annamaria.fetz@studenti.unitn.it) or to [Lucia Hrovatin](lucia.hrovatin@studenti.unitn.it) and we’ll try to help you.

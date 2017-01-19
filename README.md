# event_dataset
The event dataset arranged for ACL2017.

There are 6 files in this dataset. All of them are line based and each line uses a single line feed (LF) in the end.

[Download Page](https://github.com/acl2017submission/event-data/releases)

## mid_to_name.txt

Since freebase is closed now, we provide this file as a simple dictionary of all the entities we used in the event dataset.

There are two tab-separated columns in this file, where each line contains a **freebase entity id** and **the title on its webpage** originally. 

## key_argument_list_by_KR.txt

This file contains 21 event types and list every argument of them ranked by the KR value.

## event_instance.tsv

This file contains all the event instances in our selected 21 event types. Each line is an *instance* of an specific event type.
Columns are separated by tabs.

Each column is:

- event instance id (in freebase schema)
- event type
- arguemnts and roles they play in the corresponding event instance, formulated as role,argument. 

For example, the following line

``` text
m.0wh15c9	people.place_lived	people.place_lived.location,m.022pfm	people.place_lived.person,m.026p7hm
```

means there's a person *m.026p7hm*  lived in the location *m.022pfm*, and this event is identified as *m.0wh15c9*.

## wiki_sentence_annotated.tsv

This file contains wikipedia sentences annotated with the entities in the previous file, and also sampled sentences that cannot be annotated with the events we have (we sample about 400,000 sentences from around 17,000,000 sentences).

- **entity id**  key argument of one event instance
- **entity id**  key argument of one event instance 
- the **event instance id**  the event instance with the above two key arguments participated in. If this column is _negative_ , it means no event instance is expressed in this sentence.
- the **sentence** where these two entities occur simultaneously
- **entities** in the sentence, each of them contains three parts separated by commas and ordered by their key rate
  - the **role**  if the entity is an arguemnt of the event instance, we label it with corresponding role. If the entity is not an argument of the event instance, we label it with _negative_. And this field will be omitted if the event instance is marked as _negative_. 
  - the **entity id**
  - start and end index in the sentence of this entity. The **indices** start from ZERO and is counted when the sentence is decoded in unicode. 

For example, the following line

``` text
m.010016	m.04yg313	m.0wlqh9z	Earlie Bee Thomas (born December 11, 1945 in Denton, Texas) is a former American football cornerback in the National Football League.	people.place_lived.location,m.010016,45,58	people.place_lived.person,m.04yg313,0,17  negative,m.023wyl,90,100	negative,m.059yj,108,132	negative,m.0jm_,72,89
```

In this example, it has two key arguments(entities) _m.010016_ and _m.04yg313_, they are key arguments participate the event _m.0wlqh9z_. In this sentence, there are 5 entities marked out. 

The following line is a sentence in wikipedia that cannot be annotated with any event instance in our selected 21 event types.

``` text
m.0zwxc	m.0zxcx	negative	Monroe Elementary School is located at 1240 Boiling Springs Road in Monroe Township in Boiling Springs, Pennsylvania.	m.0zwxc,87,116	m.0zxcx,68,83
```
## wiki_sentence_annotated.with_trigger.tsv

This file is almost the same with the previous one, with the only exception that each positive example in this file contains an additional trigger annotation in the end.

We create a pseudo-property as _trigger_ for each event type, e.g.  _organization.leadership.trigger_, _military.military_service.trigger_ and so on. Each trigger annotation consists of 4 fields, namely event type of this trigger, trigger word, trigger starting and ending position in the sentence. These fields are separated by comma similarly.

The following line is an example. Note the last tab separated field is the trigger annotation talked above.

``` text
m.010rblvl	m.0hnsdkb	m.0115g5hf	She was married to the cinematographer Theo Nischwitz and was sometimes credited as Gertrud Hinz-Nischwitz.	people.marriage.spouse,m.010rblvl,84,106	people.marriage.spouse,m.0hnsdkb,39,53	people.marriage.trigger,married,8,15
```

## triggerList.zip

This file compresses 21 trigger list files for all the event types. After decompression, every file contains the corresponding trigger list for the very event type suggested by its filename. For example, the decompressed _triggerList-people.place_lived.txt_ file contains trigger words for _people.place_lived_ event.

### Task 1.1
`comunica-sparql https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me
" 
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT ?person
WHERE {                                                                                                   
   <https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me> foaf:knows ?person.
}"`

Response:
[
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/a-baumann/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/jano/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/tibor/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/Gero/profile/card#me"}
]


### Task 1.2a
`comunica-sparql-link-traversal https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me
"
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT DISTINCT ?person ?name
WHERE {
   <https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me> foaf:knows ?person .
   ?person foaf:name ?name.
}"`

Response:
`[
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/a-baumann/profile/card#me","name":"\"andreas baumann\""},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/jano/profile/card#me","name":"\"Jano Koller\""},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/tibor/profile/card#me","name":"\"Tibor Haller\""},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/Gero/profile/card#me","name":"\"Gero Traem\""}
]`

Regarding the HTTPS requests which are actually sent, we see that starting from my own card, the hyperlinks to the other cards are followed in the order as they appear above and the information about the persons is fetched from the resources.
The syntax is a reqular SPARQL query.


### Task 1.2b
`comunica-sparql-link-traversal https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me
"
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT DISTINCT ?person ?name
WHERE {
   <https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me> foaf:knows+ ?person .
   ?person foaf:name ?name.
}"`

Response:
`[
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/a-baumann/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/jano/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/tibor/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/Gero/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/jeremy/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/gandalf-justin/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/jeremy2/profile/card#me"},
{"person":"https://wiser-solid-xi.interactions.ics.unisg.ch/jeremy3/profile/card#me"}
]`

The HTTPS queries which are sent are now not only to the people designated as friends in my card but also to the friends of the other people. As there are no duplicates, it seems that already found people are skipped.
The syntax is very similar to the above, the only difference is the + after foaf:knows to indiciate link-traversal.
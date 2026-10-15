# Instructions 

Create an UML sequence diagram (using plantuml syntax) for the following scenario. 

Users of a simple question/answer app can ask questions that must start with: 

* what should I do to ... or 
* what should I do if ...

The app's backend uses NLP (Natural Language Processing) to standardize question text and then queries a curated database of answers to the most popular questions. Questions that cannot be found in the database are answered with "Hmmm... Let me think about it. Ask me again in 24 hours." The question is then saved in the database. The system's editors periodically query the database for unanswered questions. After some research, they come up with an answer with a dash of humor and sarcasm. The response is then stored in the database. Whenever a message is sent back to the customer, the app also sends an advertisement and this is how the developers earn their revenue. The app pledges to answer all questions in 24h, as long as they do not violate the app's usage policy that prohibits questions with criminal or offensive intentions.

Create an UML sequence diagram with participants: **user**, **frontend**, **backend**, **database**, and **ad server**. The **frontend** displays an input form where the user can enter their question. The question is then sent to the **backend**. The diagram should have an **alternative flow** showing paths for when an answer to the question is found in the database or not. If the question is new, it is  saved in the database. Before the **frontend** displays the answer to the question, it exchanges messages with the **ad server** requesting that a new ad be generated. The ad is then displayed with the answer. 

```

@startuml

participant user
participant frontend
participant backend
participant database
participant "ad server" as adserver

frontend -> user: Show question form
user -> frontend: Type question
frontend -> backend: Send question

backend -> backend: Use NLP to standardize question
backend -> database: Find answer
database --> backend: Search result

alt Answer found
    backend --> frontend: Send answer
else Answer not found
    backend -> database: Save question
    backend --> frontend: Hmmm... Let me think about it.\nAsk me again in 24 hours.
end

frontend -> adserver: Get new ad
adserver --> frontend: Send ad
frontend -> user: Show answer and ad

@enduml

```

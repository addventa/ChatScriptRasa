# Integration of rasaNLU in ChatScript

## Prerequisites: rasa server

First, you need to have a rasa server running with our model: **RasaModels**.

Follow the rasa NLU tutorial to deploy your rasa server.

* [rasa NLU](http://rasa-nlu.readthedocs.io/en/stable/) - *rasa NLU installation & configuration.*

You can look in the **training_data.json** to observe the rasa workout format as well as the sentences that the bot will be able to understand.

The server must run on this **IP: 127.0.0.1:5000**.

Configuration is possible in BOTDATA/**simplecontrol.top**.

## How does it works ?

Each time you will talk to the bot, the string will be sent to rasa which will process it and which, depending on his learning, will return the intent as well as the entities it will have found to the Bot in a json object.

Once we have the json object, we take the essentials, which we insert into a single string that we use like a normal user input.

So the patterns of the topics are based on the intent.
Each intention has its own subject in our case, and response models depend on entities

### The format of the string

**[intent]** **[entity]** *[entity.value]* **[entity]** *[entity.value]* ...


* intent = The intent that Bot considered most relevant.
* entity = An entity is a category of words. For example tree can be in the nature entity.
* entity.value = One or more words belonging to the detected entity.

#### Examples

```
User input: "I want to book 3 rooms with 2 beds."
New input after parsing: "'book a room' 'number of rooms' '3 rooms' 'bed type' '2 beds'"
ChatScript result: "Understood, so you want 3 rooms with 2 beds!"
```

```
User input: "Can i have wifi creditentials please?"
New input after parsing: "'wifi' 'password' 'creditentials'"
ChatScript result: "To connect to the wifi, you have to select the INDIA-X60-HOTEL, and the password is : welcomeinindia."
```


## Play with it !

The training is really light for this example so the bot will not understand everything, but if you train it with more training data, you will be able to make it really good!

The rasacall function in simplecontrol.top is where rasa is called (obvious), and you can set the minimum confidence that you think is acceptable.

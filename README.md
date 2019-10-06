# Java Alexa Skill Template

This is a basic project that should help to get up and running with creating JDK 8 Alexa Skills. 

##  Usage 

Fork this project, or download it as a zip file then import into your IDE of choice. Make changes to your groupId and 
artifactId in the pom.xml as you see fit. 

There are 5 Handlers in the `handler` package, these are the default Intents that Amazon supports, edit these as you see 
fit. They are all registered in the `BasicStreamHandler` class found in the `main` package of the template.

You will likely create more Intents with your own custom *utterances* as Amazon calls them. To add them to the project, 
place a new IntentHandler in the `handler` package ensuring that you override the following two methods from the 
`RequestHandler` interface: 

1.  `public boolean canHandle(HandlerInput input)`
2.  `public Optional<Response> handle(HandlerInput input)` 

The former is used by your skill to register whether the IntentHandler can support the request and checks the intent
name in order to do this. 

If this passes the boolean test then the second method will execute. This is where you place your custom logic for the 
Intent handler. 

---

**Example: HelloWorldIntentHandler**

````
 @Override
    public boolean canHandle(HandlerInput input) {
        return input.matches(intentName("HelloWorldIntent"));
    }

    @Override
    public Optional<Response> handle(HandlerInput input) {
        String speechText = "Hello world!";
        return input.getResponseBuilder()
                .withSpeech(speechText)
                .withSimpleCard("HelloWorld", speechText)
                .build();
    }
````

Now you've created a custom IntentHandler, you need to register it in a `SkillStreamHandler` which you can find an 
example of in the `main` package. As you'll see, the 5 basic intents are already placed there so that the skill has 
access to the basic Amazon supported Intents. Insert your custom IntentHandler as a parameter to the `addRequestHandler`
method. 

The easiest way to think of this is: 

*A **Skill** has an **Intent**. An **Intent** has a **Handler**, and is triggered by an **Utterance*** 

Within the `BasicStreamHandler` you will need to input your `SkillID`, this can be found on the Alexa Skill Console when 
you are creating your intents. This will begin with `amzn1.ask.skill.*` - ensure that you copy the full Skill ID and not 
just the section that I have omitted. 

## Maven Goal 

Execute the following goal via Maven:

`clean package`

This will produce 2 .jar files in your target directory, when you are uploading your code to AWS Lambda, ensure that you 
upload the file that does not have the `original-` prefix as this will only contain the code that you have written. 

There are a lot of tutorials online for how to upload your code to AWS Lambda, so it's not something that I'm going to 
cover in this file. 
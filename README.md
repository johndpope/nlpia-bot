# nlpia_bot

Use [NLP in Action](https://www.manning.com/books/natural-language-processing-in-action) to build your own virtual assistant that actually assists! Most virtual assistants are built to manipulate you into doing things that make money for corporations. Your personal bot can help protect you and amplify your own abilities and prosocial instincts.

This hybrid chatbot combines 4 techniques explained in [NLP in Action](https://www.manning.com/books/natural-language-processing-in-action):

    1. search: [chatterbot](https://github.com/gunthercox/ChatterBot), [will](https://github.com/skoczen/will)
    2. pattern matching and response templates: Alexa, [AIML](https://github.com/keiffster/program-y)
    3. generative deep learning: [robot-bernie](https://github.com/nlpia/robot-bernie), [movie-bot](https://github.com/totalgood/nlpia/blob/master/src/nlpia/book/examples/ch10_movie_dialog_chatbot.py)
    4. grounding: [snips](https://github.com/snipsco/snips-nlu)

The presentation from San Diego Python User Group is in [docs/](docs/2019-08-22--San Diego Python User Group -- How to Build a Chatbot.odp)

## Work in Progress

- Nima (@hulkgeek) building a question answering bot based on his state of the art question classifier
- Aliya (@beetpoet) working on a new *mystery* feature
- Hobson (@hobson) working on infrastructure (CI and deployment of webapp)
- You -- What big chatbot idea would you like to make a reality?

## Next Steps

1. movie dialog in dajngo database to hold the statement->response pairs  

    1. graph schema compatible with MxGraph (draw.io) and other js libraries for editing graphs/flow charts
    1. ubuntu dialog corpus in db
    1. mindfulness faq corpus in db
    1. famous quotes as responses to the statement "tell me something inspiring"  
    1. jokes for "tell me a joke"
    1. data science faq
    1. nlpia faq
    1. psychology/self-help faq

2. html django template so there's a web interface to the app rather than just the command line command "bot"  
3. use Django Rest Framework to create a basic API that returns json containing a reply to any request sent to the local host url, like `http://localhost:8000/api?statement='Hello world'` might return {'reply': 'Hello human!'}  
4. have the command line app use the REST API from #3 rather than the slow reloading of the csv file every time you talk to the bot  
5. use database full text search to find appropriate statements in the database that we have a response for  
6. use semantic search instead of text similarity (full text search or fuzzywyzzy text matches)  
    6.a add embedding vectors (300D document vectors from spacy) to each statement and response in the db  
    6.b create a semantic index of the document vectors using `annoy` so "approximate nearest neighbors" (semantic matches) can be found quickly  
    6.c load the annoy index of the document vectors every time the server is started and use it to find the best reply in the database.  
    6.d use universal sentence encodings instead of docvecs from spacy.  
7. create a UX for dialog graph creation/design:  
    7.a install [mxgraph](https://github.com/totalgood/mxgraph) in the django app  
    7.b create a basic page based on this mxgraph example so the user can build and save dialog to the db as a graph: [tutorial](https://jgraph.github.io/mxgraph/docs/tutorial.html#1), [example app](https://jgraph.github.io/mxgraph/javascript/examples/grapheditor/www/index.html)
    7.c convert the dialog graph into a set of records/rows in the nlpia-bot db so it acts  
8. tag different dialog graphs in the db so the user can turn them on/off for their bot  
    8.a allow the user to prioritize some dialogs/models over others  
    8.b allow the user to create their own weighting function to prioritize individual statements produced by the api  
9. train a character-based generative model
    9.a decoder half of autoencoder to generate text based on docvecs from spacy  
    9.b decoder part of autoencoder to generate text based on universal sentence encodings  
    9.c train model to generate reply embeddings (doc vecs and/or use vecs) using statement embeddings (dialog engine encoder-decoder using docvecs or use vecs for the encoder half  
10. add a therapy/mindfulness-coach feature to respond with mindfulness ideas to some queries/statements
11. add the "translate 'this text' to spanish" feature  
    11.a train character-based LSTM models on english-spanish, english-french, english-german, english<->whatever  
    11.b add module for this to the django app/api  
12. AIML engine fallback

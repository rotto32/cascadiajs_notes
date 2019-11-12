# CascadiaJS 
##### Nov 8, 2019 - twitter #cjs19
#### Table of Contents
[Opening Comments](#opening-comments) \
[Talk 1: When Porgs Scream at Webpack](#Talk-1) \
[Talk 2: Controlling Drones with JS](#talk-2) \
[Talk 3: Creative Architectures: GraphQL, REST & Netlify Serverless](#talk-3) \
[Talk 4: Building an API Composition Layer](#talk-4) \
[Talk 5: Tackling the Tradeoffs of GraphQL](#talk-5) \
[Talk 6: Faster Dev w/ Gatsby ](#talk-6) \
[Talk 7: Builing a Faster, Lazier Stack](#talk-7) \
[Talk 8: Accessibility is a Hydra](#talk-8) \
[Talk 9: How to Breakup with a JS Library](#talk-9) \
[Talk 10: Machine Learning for Frontend Devs](#talk-10) \
[Talk 11: Futuristic Code Bases](#talk-11)



----

## Opening Comments
They have a live stream at 2019.cascadiajs.com/live.

Tougo Coffee provides coffee. Locations in Central District, First Hill.

### Scholarship Program - 
Fundraising \
$1,750 from non-hoodies ($50/person) \
$2,200 from individual contributions \
$23,900 from sponsor contributions (some unsolicited) \
$27,860 in total, record for CascadiaJS

Number of Scholarship Recipients \
2017 - 6 \
2018 - 48 \
2019 - 100 

People from as far away as Amsterdam here.

----

## Talk 1 
## When Porgs Scream at Webpack - 3 ways to use JS w/ hardware
### Speaker: Dominic Kundel (he/him) @dkundel
#### Subjects: Hardware hacking, Serial Port, Johnny Five, Tressel
#### TLDR: Wrote progjs to make electronic toy move when webpack build fails
#### Links: 
github.com/dkundel/porgjs \
https://github.com/dkundel/porgjs
#### Notes:
Destiny of hardware - obsolete
Hardware hacking isn't easy - require preparation, specialized tools and parts, more expensive than software, there's no undo

1. API's & Protocols \
JS=> API => C/C++ => Hardware \
API Options \
1: Particle, can use curl to access \
2: MQTT protocol that's machine to machine. Don't need to know IP. Cross platform \
  -> connect and setup subscribtion, C loop, and callback \
Example: setup light to tell if roommate was on Twitch so he could be quiet

2. Tethered Node ports \
Serial Port and Johnny 5, but you have to be tethered to a host machine. And the machine needs to be capable of running NOdeJA. BUt the code is super user friendly.\
To get around the issue with having to be connected to a machine, and used a porg toy that moves to move when a build fails \
LEDs are the console.log of hardware \
example: porgjs creates a port to the hardware \
PROs: familiar tools, easy, hardware independent \
CONs: tethered to a host

3. Untethered Nodebots \
Run js on hardware - JerryScript lightweight -limited functionality, not beginner friendly \ 
Espruino - JS processor(?) opensource, IDE, but doesn't work with Johnny5 \
Neonius - supports Typescript and Node.js \ 
Tessel - Node.js, JS, expensive
example: hacked a coffee machine - used Tessel


____


## Talk 2
## Controlling Drones with JS
### Speaker: Jasper Schulte (he/him) @zjaaspoer
### Subjects: Drones, hardware
#### TLDR: How to of programming drones
#### Links:
jaspershulte.nl 
#### Notes:
From Amsterdam, consulting w/ TripAdvisor

Process
1. Choose the right drone \
  A Brief History of drones \
  -> Old days had to solder your own drone \
  -> RTF (ready to fly) $$$$$ \
  -> Cheap drones\
Want somethign cheap and can fly indoors, not dangerous, and an interface for control \
Recommended drone: RyzeTech Tello $100 

2. control one drone \
Need to tell whether or not you're moving, and in what direction -> used bedcovers b/c downward facing camera \
Sending commands & recieving telemetry - UDP for communication, doesn't have response \
Hardware is very unpredictable, and has physical limitations, not super great feedback \ 
can get live info from drone 

3. control swarm of drones \
most important info is knowing the relative positions of drones \
use 'mission pad' for downward facing camera so that each drone knows where it is \
calculate relative position 

Controlling drones is hard b/c they don't have good sensory input, lots of external factor. Need your own feedback system (like mission pads)

Hold a drone like feeding a horse
____

## Talk 3
## Creative Architectures: GraphQL, REST & Netlify Serverless
### Speaker: Hannah Ingham (she/her)
### Subjects: GraphQL, APIs
#### TLDR: GaphQL makes APIs faster and more efficient
#### Notes:
Slalom, Bootcamp grad

GraphQL -  query language for APIS, by Facebook, replacement/compliment to REST APIs
very popular, lots of tools for GraphQL, Apollo, AppSync, etc \
Why build with GraphQL? -
Reduces # of calls to network. Limit over and underfecthing b/c its more specific. Makes calls quicker & more efficient, and get a lot of control over your data \
GraphQL is optimized for reads, and can expose GraphQl on existing infrastructure, can use on momlithic and serverless architecture \
Example: Card Monkey - serverless, graphql, netlify (good way to expose yourself to lambda functions). Used REST for post, put and delete, but graphql for get. \

Call to action: do personal projects in structureless environment where you can make decisions and help you learn
____

## Talk 4
## Building an API Composition Layer
### Speaker: Brea Gaudioso (she/her) @breagaudioso
### Subjects: API, architecture, optimization
#### TLDR: Use one user-facing layer to be consitent and make sure you version and doc it
#### Links:
#### Notes:
Expert at consumer-facing APIs

APIs should be easy to use. Integrating w/ 3rd part API can suck. Usually due to documentation being an afterthought, inconsistencies (due to inability to change structure afterwards), different engineering visions.

Compostion layer is the API gateway, customer facing layer, one point of contact, covers up the flaws of deeper laysers of the API. 

Wnat your compostion layer to be super consistent and predictable, so that it is easy to use. \
   Benefits: \
  Caching \
  Validation \
  Monitoring of use b/c of centralized point of entry \
  Centralized auth \
  Single schema to integrate 

  Method: \
  Pick an architecture & parameters - Pick & stick \
  -> SOAP, pagination, etc \
  Use versioning & be consistent, use a change log \
  DOCUMENTATION - API is only as good as the docs \
  -> recomend open source documentation tool \
  -> treat documenation as part of dev process \
  -> developer sandbox tool \
  -> use examples \
  -> developer portal awards 

  Keep it consistent, keep it simple.

____


## Talk 5
## Tackling the Tradeoffs of GraphQL
### Speaker: Tre Ammatuna (he/him) @tretuna
### Subjects: Caching in GraphQL
#### TLDR: GraphQL, being flexible, is jsut more difficult to cache, but it is possible with libraries
#### Links:
#### Notes:
frontend Leafly
GraphQL - Uncachable? - No!

Why GraphQL - faster & more efficient

Tradeoffs - thought debt of shifting to data graph mentality
caching is different in GraphQL

Client side - fetching: use isomorphic fetch
using library like Relay, Apollo, or URCL - come w/ denormalized cache so you don't have to worry about caching on client-side

Resolvers - how you get data
w/ REST API this is code you've written
GraphQL has a resolver that is also code you've written, so you can add a cache
Use Facebook dataloader for single request caching. Batches mutliple calls & caches them for you. But this is onely database side

So for REST and GraphQL you can use Apollo data source in a class that has a default LRU cache

Biggest issue - transfer protocol: 'You can't cache a POST request' - actually you can, whether or not you should. GraphQL doesn't care about protocols - all it does is it get the request there.  \
Persisted queries turns a post request into a get request, and then you can cache get request. Client saves post id as hash, client sends GET request w/ post hash for caching. Results in client driven APIs - GraphQL allows fronted devs to move quickly.

GraphQL, being flexible, is just more difficult to cache, but it is possible with libraries


____

## Talk 6: Faster Dev w/ Gatsby 
### Speaker: Daniel Lemay (he/him) @dslemay
### Subjects: Gatsby, Preformance
#### TLDR: Gatsby is an easy and performant way of building sites
#### Links:
slideshow dsl.cx/gatsbythemes
#### Notes:
Dev at Phase2
Move from static HTML, handcoded

Gatsby - plugin framework that wraps around React for performance - takes care of code splitting and compiling, good plugin integration, very performant

What about reusability? - Gatsby themes to keep things dry. Stable as of this year. Originally had some issue with github integration and couldn't get updates b/c starter will rewrite git history. Themes are managed more like npm packages

Using a theme - install a theme like a plugin.

Plugins are basically used for all reusable code. 

Gatsby theme can be an object or a function, so you can pass in a key, for example, and it can insert into theme

Shared global providers - wraps entire application to provide different contexts depending on variables

Increase UI Reuse

____

## Talk 7
## Building a Faster, Lazier Stack
### Speaker: Samantha Siow (she/her)
### Subjects: React, Optimization, Architecture
#### TLDR: Made slack 33% faster with loading less code, having less local data, and prioritizing API calls
#### Links:
samanthasiow.com
#### Notes:
Senior front end engineer at Slack.

Slack was launched in 2014 with Handlebars and Smarty, jQuery, nultiple process for workspaces (ie more CPU usage for more workspaces).

2017 migrated to React.

In 2019 Slack has 10M daily users, and many more devs.

Comparison of legacy vs modern slack app

All UI components built in React
  Single process for multiple workspaces (uses less CPU), 33% faster


Optimizations
1. Load less code upfront \
  Initially downloaded all JS required to run app, and then all assets - 1750ms in all \
    As expanded more assets, slowed down \
    Inaccesible while fetching assests \
  In modern app, (look up blog post about Gantry), initial JS download went from 750 to 160ms, overal down to 800ms \
  start API call sooner \
  Service worker caches assets 160ms to 36.9ms, bringing the total to 550ms, and useable in low connectivity environments\
  Code splitting to bundle assets to download in parallel 

2. Declutter boot data \
  have loads of data, need to download a ton of data before app could be useable \
  On front-end reduced the amount of data being fetched from API
  Originally they would complete model and would fetch on events, and was fetching all data at boot time \
  Moved to only fetching data as need. Started with initial data fetch and fetch other data as needed \
  Example: viewing a message mentioning a user that's not local to your app - will look in redux initially and then fetch the data if necessary \
  Lazy-loaded incomplete data model and fetch on demand

3. Prioritize initial API calls
  certain calls block boot and need to be done before app can load \
  More strategic about API calls
  Originally there were 3 calls before the app is completely booted and there were non-blocking calls happenign between blocking calls \
  Updated to have the high-priority calls first and only calling thing that were absolutely necessary. And called them in parallel with initial JS \

  Takeaways: Load less code upfront, small boot payload, code splitting to allow having JS in small bundles that could be paralized, use SW to cache \
  Fetch data on demand, lower memory storage\
  priotizing initial API calls & front loading, parallizing calls, start blocking API calls first



____

## Talk 8
## Accessibility is a Hydra
### Speaker: EJ Mason (they/them) @codeability
### Subjects: Accessibility, abliesm, Social justice
#### TLDR: Websites continue to have acessibility problems because society is ableist
#### Links:
Tatiana Mac - Systems of Systems \
Vilissa Thompson 
#### Notes:
Sr software dev at Webflow

The battle with the hydra is one of fighting the same thing over and over again

WCAG is the accessibility guideline written by W3C 

Kinds of issues seen before:
using onclick event handle on span - unclear to non-mouse users => turn span to button and allows screen readers and keyboard users

overuse of large blocks of texts - hard to to navigat => use headings in addition

The problem was that EJ would see the same problems over and over again even after solving them the first time

The reason that this keeps happening is because we are solving problems in a way that allows these problems to persist. We often tell stories where the ppl that the stories are about are not involved in the telling of the stories.

Representation matters.

It is important that the people who build websites have an eye towards not only making websites more accessibility, but also work to dismantle ableism

Listen to more people with disabilities, work towards being anti-ableist (work towards making more things in life accessible and commiting to work towards accessibility)


____

## Talk 9
## How to Breakup with a JS Library
### Speaker: Daria Caraway (she/her) @darcar31
### Subjects: React, DRY, reducing tech debt
#### TLDR: When using libraries ensure that you're only using a single point of access to libraries
#### Notes:

Software engineer at Workday

Process of using a library 
Everything is great -> using it everywhere -> dependent on it

Lots of reasons to 'breakup' with a JS library

Often times people will scrub the library out of the code base, or use the old deprecated version of the library but not touch it, or piece by piece update but then your code is fragmented

To avoid:
1. prototype multiple libraries early
  Teaches you 
    how you interface with the library
    Compares different libraries
    Learn about deisng and coding styles in the library
    Your expectations around customization, performance, etc
    Features needed now and in the future
    Share prototypes with shareholders and coworkers, etc

2. Structure code to be able to quickly switch out libraries
  Use Wrapper components
    Tools: TypeScript, React or Not using a typing system? JSDoc \
    Basically when you import a piece from a library you wrap that import into whatever system you're using, prop-type it, and pass in props to the wrapper, and when you update your library you just have to change the wrapper. You can also write a custom component with a wrapper that simply doesn't have a library, and plug in a library later

3. Writing tests
    When writing tests don't test on library specific features, but on things you control

When updating libraries you can go into your wrapper and just update the bit about the library


So, basically, use libraries like variables - instead of sprinkling them in your code, use a wrapper that is then used throughout the actual code so that all you ever need to do is change the wrapper

The other benefit of this is that it makes the use of the library itself much more flexible - your actual code base can be standardized without having to bend to the standards of the libraries you're using



____


## Talk 10
## Machine Learning for Frontend Devs
### Speaker: Charlie Gerard (she/her) @devdevcharlie
### Subjects: Machine learning, front end dev
#### TLDR: Machine learning is available as a realatively easy-to-use tool for web developers to create innovative and time-saving applications.
#### Links:
https://teachablemachine.withgoogle.com/
#### Notes:

Frontend dev at Atlassian, Google Dev expert and Mozilla Tech Speaker

What is machine learning? - Giving the ability to computer to find patterns in data without being explicitly programmed. 

You create models functions which are created with algorithms. You don't have to understand the math behind the algorithms, but knowing what they're good for is useful.

Looking at two types of machine leanring - supervised and unsupervised

1. Supervised
    Created predictive model based on a set of features and labels \
    Example: you have data for the cost of all the houses in Seattle, trying to predict when to sell a house. The predicitive model is some sort of function which takes in new inut (such as the house you're curious about) and the output is when you should sell based on previous data

2. Unsupervised
    The ability to create predictions based only on a set of features \
    Will cluster things together - get a lot of unrelated data that can cluster that data together to draw general conclusions about that cluster
    Example: taking shopping data you can tell gender, socio-econmonic status, etc

Cool uses of machine learning - generated alt text from image, check if image is NSFW, train Alexa to learn sign language (interpret visual inputs)

Using Machine Learning w/ JS \
Why: \
Accessible, easier learning curve \
Rapid prototyping \
Big ecosystem 

What: \
Import pretrained model \
retrain imported model \
Define, train and run models entirely in the browser (not recommend) 

Tools -
TensorFlow.js, Kera.js, MagentaJS, Teachable machine

Demos: \
Use camera to tell if something is recyclable or not \
  -> using a pretrained model cocoSsd from tensor-flow \
Use handmotions to type on keyboard \
-> retrained mobilenetModule from tensor-flow \
Use hand motions to play games 

Limits: 
+ Need large amount of data
+ Can take a lot of time to train your own model
+ Think about mobile experience - some models are very heavy. This will likely improve in the future
+ Liability (some models are black boxes)
+ Bias and ethics - humans are biased and humans make the algorithms, so there you go

____


## Talk 11
## Futuristic Code Bases
### Speaker: Brian Holt (he/him) @holtbt
### Subjects: WebAssembly, VS Code, Azure, Lambdas, Webflow
#### TLDR: Web development is getting more abstract and accessible for people of less traditional backgrounds, but still requires people w/ more 'traditional' skills to make those tools
#### Links:
aka.ms/vsfutures-signup
#### Notes:

Program manager for NodeJS on Azure at Microsoft and VS Code

Predictions:
1. Backend will own more frontend
    More demographics into the frontend of dev
    Blazer - write C# and run in browser using WebAssembly (ppl excited about WebAssembly). Blazer runs almost entirely on the server or on the client depending on your needs. \
    Brian expects that there will more more languages in the front end besides JS \
    Some considerations on this:
    + JS is a really good front end language
    + ppl are already good w/ JS
    + WebAssembly is limited

2. Frontend will own more backend
    Getting easier and easier to use backend \
    Serverless development is up and coming - serverless means you're building per invocation and you don't have to manage your own instances - Azure, AWS Lambda, etc \
    The progression has been from onsite server machines -> AWS EC2 -> Heroku/ Elastic Beanstalk -> Lambda functions \
    With serverless you only manage the business logic of an application \
    As a developer you offload the stuff you don't care about \
    Things you should try:
    + Lambdas, Azure functions, etc

3. Everyone will have more access to code
    No code revolution is coming - it will be easier for more people to build software with more intuitive tools \
    Tools like Webflow \
    Increases productivity and accessibility \
    But it also means that web coding is getting more abstract \
    We will also still need to have people to build those abstraction layers \

4. The future of codign tools
    Developing in containers \
    allows for thin clients \
    reproducible dev environment \
    app built in the same environment in which its deployed \
    Note: Docker isn't scary, Kubernetes is scary


Demo: VS code has functionality which will automatically spin up the dev container and open the VS Code in the container. It can also manage port mapping in the vs code GUI. Requires Docker & lots of memory, etc

VS Studio online can spin up dev environment and then using the local installation of VS Code and you can be using the remote dev environment on any client that you want 

Oooh ppl talking about Vagrant in past tense

____



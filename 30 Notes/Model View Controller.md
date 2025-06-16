---
created: 2024-04-22 18:33
modified: 2025-06-15T18:52:47-04:00
alias:
---
source:: [Hacker Way: Rethinking Web App Development at Facebook - YouTube](https://www.youtube.com/watch?v=nYkdrAPrdcw&t=624s)
[Flux vs MVC Design Pattern. In Web Application development MVC is… | by Madasamy M | Medium](https://madasamy.medium.com/flux-vs-mvc-design-pattern-de134dfaa12b)
# Model View Controller

The MVC (Model-View-Controller) diagram illustrates a software architectural pattern for implementing user interfaces by separating the application into three interconnected components. Here is how it works step by step:

1. **Action**: The process begins when the user performs some action in the interface (such as **clicking a button**, submitting a form, etc.) that requires processing or retrieving data.

2. **Controller**: The action is then taken up by the Controller, which interprets the user's input and makes decisions on what to do next. It acts as the intermediary between the Model and the View. After the controller decides what data manipulation or retrieval is needed, it communicates with the Model.

3. **Model**: The model is in charge of fetching, storing, and manipulating data (typically from a database or another data source). The Model processes the data as needed and returns it back to the Controller.

4. **View**: Once the Controller receives the data from the Model, it prepares and formats this data for presentation. It then selects the appropriate View, which is the presentation layer that the user will interact with. The View displays the final user interface (UI) to the user, with the data provided by the Model.

Example:
Let's take the example of a simple blog application.

**Action**: A user wants to read an article, so they click on the article's title on the homepage.

**Controller**: The article's title click event is captured by a Controller, which identifies that the user wants to view a specific article.

**Model**: The Controller retrieves the article's ID from the request and asks the Model to fetch the article's content from the database.

**Model**: The Model queries the database for the article's content using the article ID, retrieves it, and sends it back to the Controller.

**Controller**: With the article's content now retrieved, the Controller prepares the data and decides to send this data to the Article View.

**View**: The Article View is then populated with the article's content and rendered in the user's browser, presenting the completed article ready for reading.

In this example, the Model is the part of the app concerned with the data of the articles, the View is the presentation layer that displays the articles, and the Controller acts in between to control the flow of data to and from the Model and the View.


**Linked References to this Note**
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```

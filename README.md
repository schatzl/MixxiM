# :seedling: Beet Anything
A one-hour vibe coding project

Web app to easily select matching vegetables for mixed bed cultivation

## Motivation

Private vegetable gardens typically consist of a number of beds that are cultivated differently each year.

One reason for this is that vegetables differ in how many nutrients they need while growing. Soil that has been used to grow a plant with a high nutrition demand usually doesn't regain these nutrients in a single season. Hence the same plant can't be grown again in the same place in the next season.

The second reason is that some species of plants and also their roots and remnants in the soil can have infavorable influence on other plant species. This can prevent them to grow properly, thus they have to be kept apart. On the other hand, there are certain plants that mutually improve the growth conditions y when grown together.

Therefore its a recurring, natural thing to plan the beds in spring by means of plant tables. 

The motivation for writing this code is making the whole process easier, in particular over the course of several years. An important part will be a suggestion algorithm based on a set of given vegetables (i.e. kind of a wishlist).

## Development stages

The initial code contains 
- a lean class hierarchy representing different logical entities within an orchard
- a data structure containing compatibility information for a basic set of vegetables
- any functionality to model a orchard on the commandline
- code to persist data 

A second step will integrate
- a slim web interface built with streamlit to modify the vegetable information
- a readonly web interface to show the complete vegetable matrix

Advanced features will be
- a suggestion algorithm for ideal combinations, based on a given set of vegetables
- multi-season consideration of crop rotation
- the possibility to define some kind of individual rule set

The final application will contain
- a graphical representation of the orchard
- drag and drop functionality for creating a patch including suggestions

© 2023, SCHATZL

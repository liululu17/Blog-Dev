---
title: "Transportation Modeling 101"
summary: What are the objectives of transportation modeling? How many different technical approaches to reach those objectives?  
date: 2025-05-17
series: ["Intro"]
weight: 1
aliases: ["/TM-101"]
tags: ["Transportation Modeling", "Statistics"]
author: ["Lulu Liu"]
cover:
  image: 
  hiddenInList:
social:
  fediverse_creator:
---

This is a introductory blog to help public understand the application of transportation modeling in industry under a big picture view, but will not include more details. It overall introduce 2 main models by different development objectives: planning and business. So they are using different technical approaches and methods to develop and apply models. 

 **Reader could regard this blog as an index**. The table / mind map provide the referenced paper, report, book chapter that explore specific theory or methods (for reader explore more)

---

## Why We Model Transportation

A model is a  simplified version of real world. basically, it is a digital world trying to simulate the complex movement, activity, Phenomenon of nature and human society from real world. we use model to help understand better about our surroundings. Imagine building a “digital twin” of a city: a simplified, virtual version that simulates real-world movements—like traffic patterns, delivery routes, or commuter behavior. That’s what transportation models do. They help us answer questions like:

- What if we build a new subway line?

- How can we avoid traffic jams?

- Where will ride-hailing demand spike in the next hour?

But no model can capture reality perfectly. We build models based on specific goals, and those goals decide what data we collect, what math we use, and how we train or simulate the model.

Model varies based on its objective and purpose. what mathematical models should be applied, what data inputs should be used in model, how to set up parameters and train models, all these questions are all based on what we need from the model.

Let’s say you want to:

- Predict a traffic jam — you’ll need up-to-date traffic data and a model that reacts in real time.

- Estimate how many passengers need a ride downtown — you'll need demand data, time patterns, and perhaps weather or event info.

- Explore how transit fares affect travel choices — you’ll focus on long-term behavior trends and simulate different policy scenarios.

These different goals lead to different modeling strategies. This blog introduces two main purposes of modeling—city planning and business decision-making—and how each uses different techniques, from classic statistical models to cutting-edge machine learning.

### Two main purposes of modeling

**Business model**

Transportation models used by companies—like Uber, Amazon, or delivery fleets—are designed to **maximize operational efficiency and profit**. These models aim to predict demand, suggest efficient delivery routes, reduce travel time, and improve customer experience. Since decisions often need to be made in real time, these models require **high accuracy, real-time updates, and flexibility**. 

To meet these demands, companies often rely on **machine learning** approaches, including advanced methods like **Graph Neural Networks (GNNs)** and **Transformers**. These models can process large amounts of dynamic data, such as GPS traces, traffic sensors, and weather updates, to make fast and accurate predictions. The downside is that these models may be less interpretable—businesses care more about performance than full transparency.


**Planning Model**

Public agencies and city planners use transportation models to support **long-term infrastructure and policy decisions**. The goal here is to understand how people make travel decisions and how different factors—like transit prices, travel time, or land use—affect travel patterns. These models help answer questions such as: Should we build a new transit line? How will tolling a freeway affect traffic volumes?

Planning models prioritize **transparency, interpretability, and the ability to test policy scenarios**. They don’t need to operate in real time, but they must be reliable over the long run. Because of this, planners often use **statistical models** and **simulation frameworks** like the **Four-Step Model** or **Activity-Based Models (ABM)**. These models may not be as precise as real-time machine learning systems, but they offer a better understanding of underlying causes and relationships.

#

| Aspect              | Business Modeling                                | Planning Modeling                              |
|---------------------|--------------------------------------------------|------------------------------------------------|
| **Goal**            | Maximize profit and efficiency                   | Support long-term public decisions             |
| **Users**           | Private companies (e.g., Uber, Amazon)           | Public agencies, urban planners                |
| **Requirements**    | Real-time, high accuracy, flexible updates       | Transparent, interpretable, stable over time   |
| **Technical Methods** | Machine learning (GNNs, Transformers, etc.)     | Statistical models, 4-Step Model, ABM          |
| **Data Type**       | Dynamic, real-time GPS, traffic, user demand     | Survey data, census, land use, network design  |
| **Update Frequency**| Frequent (hourly or daily)                       | Occasional (monthly, yearly, scenario-based)   |
| **Model Transparency** | Lower (black-box models)                     | Higher (clear assumptions and logic)           |



#

In the next section, we’ll explore the common technical approaches for these two fields:

---

## Planning Model -- mathematical model

### Demand network and Supply network

Transportation planning revolves around two core elements. 

**Demand**: The travel needs and behaviors of individuals and households. 

**Supply**: The transportation infrastructure available, including roads, transit systems, and other facilities.

Models like the Four-Step Model and ABM are tools used to simulate and analyze how these two elements interact, helping planners make informed decisions about infrastructure investments and policy implementations. In one sentence, models aim to explore how to plan supply network to satisfy travel demand under certain conditions.

### ABM & 4 steps

Developed in the 1950s, the Four-Step Model is a sequential process that estimates travel demand and assigns it to the transportation network.[^1] This model treats trips as isolated events, focusing on aggregate flows rather than individual behaviors. The steps include:

[^1]: Travel Forecasting Resource [Trip-based models](https://tfresource.org/topics/Trip_based_models.html)

1. Trip Generation: Estimating the number of trips originating and ending in different zones.

2. Trip Distribution: Determining where trips go, linking origins to destinations.

3. Mode Choice: Deciding which mode of transportation (car, bus, train, etc.) is used.

4. Traffic Assignment: Allocating trips to specific routes within the network.

![alt text](https://i0.wp.com/transportgeography.org/wp-content/uploads/four_stages_tlu_model.png?resize=1024%2C460&ssl=1)


ABM takes a more detailed approach by simulating individual daily activities and travel behaviors. It considers:

- Individual Schedules: Modeling the sequence of activities (work, shopping, school) for each person.

- Household Interactions: Recognizing that household members coordinate activities and share resources.

- Time and Space Constraints: Accounting for the timing and location of activities, leading to more realistic travel patterns.

By focusing on the underlying reasons for travel, ABM provides a nuanced understanding of demand and its interaction with the transportation supply.

Think of the Four-Step Model as a static photograph capturing the number of vehicles between two points during rush hour. In contrast, ABM is like a documentary film following individuals throughout their day, revealing the motivations and sequences behind each trip.

| Aspect               | Four-Step Model                              | Activity-Based Model (ABM)                     |
|----------------------|----------------------------------------------|-----------------------------------------------|
| **Demand Representation** | Aggregate trips between zones.         | Individual activity patterns and schedules.   |
| **Supply Interaction**    | Assigns trips to network based on volume. | Simulates individual routes considering time and mode. |
| **Behavioral Detail**     | Limited; does not account for trip chaining. | High; includes trip chaining and activity dependencies. |
| **Temporal Resolution**   | Often peak periods or daily totals.     | Detailed time-of-day analysis.                |
| **Data Requirements**     | Less intensive; relies on zonal data.   | High; requires detailed individual and household data. |

#

MPOs are regional agencies responsible for transportation planning in urbanized areas. Here's a snapshot of some major MPOs and the models they employ:
#

| MPO Name                                      | Region Covered             | Model Type         | Notes                                                                 |
|-----------------------------------------------|----------------------------|--------------------|-----------------------------------------------------------------------|
| San Diego Association of Governments (SANDAG) | San Diego, CA              | Activity-Based     | Utilizes an advanced ABM for regional planning.                       |
| Metropolitan Transportation Commission (MTC)  | San Francisco Bay Area, CA | Activity-Based     | Employs ABM for detailed travel behavior analysis.                    |
| Metropolitan Washington COG (MWCOG)           | Washington, D.C.           | Four-Step          | Uses a traditional model but exploring ABM integration.               |
| New York Metropolitan Transportation Council (NYMTC) | New York, NY       | Activity-Based     | Implemented ABM for comprehensive planning.                           |
| North Central Texas Council of Governments (NCTCOG) | Dallas-Fort Worth, TX | Four-Step          | Uses traditional model with enhancements; considering ABM adoption.   |


## Business Model -- Machine Learning
main models used for
### crowd-sourced road traffic 
Waze, CityMapper: provide better transit route for users

### Google GGN for travel time prediction and roue planing 

## Learn from Both
### Summary
compare expert model & ML/DL model

---


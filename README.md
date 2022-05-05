# Watershed challenge

### Important points to take into account:

This challenge shouldn't take more than 5 hours, so we don't expect perfect answers.
The difficulty will grow, so try to answer as much as you can. For the same, it is not mandatory to complete the whole challenge.

Only will be accepted Jupyter notebook/lab files and they need to run from the beggining to the bottom.

# Motivation

Note: the following paragraph is only for understanding the problem and why is relevant. It is not necessary to fully understand the background, the challenge itself will guide you. So read fast this information and follow with the challenge.

The heat waves are extreme meteorological events (extreme temperatures) which can impact negatively in our ecosystem. This impacts abroad from very hot summer days and wildfires to floods and alluviums. As the heat waves answer to atmospheric circulation phenomenas, which can be detected few days in advance, there is a big opportunity for trying to predict the occurrence of the negative impacts associated to this phenomena. This is key in the context of global warming, where the frequency of this events have grown in the last century ([https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2012GL053361](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2012GL053361)). For explore the opportunity of predict heat waves, in particular the peak-flows events (in extreme cases could be river floods), in Chile there are a big monitoring network of hydro meteorological variables. Thank to public institutions as DGA and CR2, we have data from different stations, some of which measure temperature and precipitations, and others measuring the total water that a hydrographic watershed contribute to a section of river. 

Some of the key questions we could try to answer are:

- Has increased the frequency of heat waves events? For this we should analyze temperature information.
- There is exist a relationship between heat waves and peak flow events?
- If yes, can we explain this event because of the watershed's features?

# Instructions

As we discussed above, we will try to predict extreme watershed events in Chile. For this we count with a public and real dataset from meteorological stations.
Each row represent the measure of daily flux in a specific station. This measure will be associated with watershed's features (fixed) and daily temperature and precipitation measures of nearby stations.

The file flux.csv contains all the data used for this challenge. This database was produced by us and synthesize flux, temperature and precipitation data.

Note about the database: the stations which measure flux and the stations that measure temperature and precipitation are not located at the same place. For building this database, we take the watershed's upstream polygon and find the temperature and precipitation stations inside this polygon, and we calculate the average over that variables. In this way, every flux measure will be accompanied of an unique temperature and precipitation measure (there's possible to have flux measurements without temperature or precipitations).

The base contains the following variables between others:

- station_code: station code
- station_name: name of the watershed
- date: date of measurement
- flux: water flux for that day
- avg_precip: average precipitation for that day in that watershed
- avg_max_temp: maximum average temperature for that day in that watershed

## Challenge

1. Download the file flux.csv from github
2. Perform an EDA over flux.csv file.
3. Plot flux, temperature and precipitations:
    1. Write a function that plot a time serie of a specific variable (flux, temp, precip) from a station. Should look like this:
        
        ```python
        def plot_one_timeserie(cod_station, variable, min_date, max_date):
        ```
        
    2. Now write a function that plot the 3 variables at the same time. As the variables are in different scales, you can normalize before plotting them. Should look like this:
        
        ```python
        def plot_three_timeseries(cod_station, min_date, max_date):
        ```
        
4. Create three variables called:
    - flux_extreme
    - temp_extreme
    - precip_extreme
    
    This variables should take the value 1 when that variable in a specific day was extreme. Being extreme could be considered as being greater than expected, so for example, a flux we can be considered as extreme (value 1) when is over the 95 percentile of the flux distribution for that specific season, and takes the value 0 otherwise.  Taking into account the seasonality of that variables is very important, because $25^\circ C$ could be considered as extreme in wintertime, but it’d be a normal temperature for summertime.
    
    Do you consider this a good way of capturing extreme events? Or you would have used a different method? Which one?
    
5. Analyze the variable flux_extreme. Are different the behaviour of different watersheds?
6. Plot the percentage of extreme events during time. Have they become more frequent?
7. Extreme flux prediction. Train one or many models (using your preferred algorithms) for estimating the probability of having an extreme flux. Feel free to create new features or use external variables. Some of the discussion we would to see: Which data we can use and which cannot? Of course, we cannot use future data, but what about data from the same day? Or from the previous day? 
    
    Everything depends on how you propose the model use. Make a proposal on how you would use the model in practice (for example, once trained, the model will predict next day probability). Depending on your proposal, set constraints about which variables you can o cannot use.
    
8. Analyze the model results.
    1. What is the performance of the model? Which metrics you consider are the best suited for this problem? What are the most important variables? What do you think about the results?
    2. If we wanted to identify at least 70% of the extreme flux events, which are the metrics of your model for that threshold? It is a useful model?
9. Upload your work to a public repository (MIT licence desired) and send the link to us to our email YYYYYY with the subject “Watershed challenge”

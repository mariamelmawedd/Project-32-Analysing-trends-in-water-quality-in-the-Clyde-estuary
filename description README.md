# Project-32-Analysing-trends-in-water-quality-in-the-Clyde-estuary

Overall project description
The Scottish Environment Protection Agency (SEPA) has a statutory obligation to monitor the state of the environment. As part of that duty, water samples are taken regularly from sampling stations along the River Clyde. Data are available for a twenty year period from the mid-1970’s until the mid-1990’s. A natural measure of water quality is dissolved oxygen (DO). There is interest in identifying the pattern of DO along the river, the nature of any time trends and the relationship between DO and physical variables such as temperature and salinity. Data are also available at different depths. The aim of the project is to use this information to provide a description of how the health of the estuary has changed over this 20 year period.

Individual project details
How many individual projects are available in this area: 1.

Data available
Data are available on dissolved oxygen at a variety of sampling stations up and down the river and at different times of year. Measurements of temperature and salinity are also available. Over the 20 year period there are 11085 observations. The data are stored in the text file clyde.dat. The code below reads this and creates a dataframe.

temp     <- scan("clyde.dat", na.strings = "*")
temp     <- as.numeric(temp)
d        <- matrix(temp, ncol = 15, byrow = T)
d        <- as.data.frame(d)
d        <- d[ , 1:13]
names(d) <- c("Station", "Day", "Month", "Year", "Stime", "HWGMT",
              "LWGMT", "Tidal", "Depth", "Temp", "Salinity", "DO", "sat")
d$id     <- factor(d$Day * 10000 + d$Month * 100 + (d$Year - 1900))
d$doy    <- cumsum(c(0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30))[d$Month] + d$Day
d$year   <- d$Year + d$doy / 365

The dataframe d contains the following columns:

DO - a measurement of dissolved oxygen.
Station - the location of the sampling station, expressed as the number of miles downstream from the city centre.
Day, Month, Year - the date the measurement was made.
doy - the day of the year (0 - 365) the measurement was made.
year - the time of the measurement on the year scale, including the proportion of time through the year corresponding to the day of the measurement.
Depth - the water depth at which the measurement was made.
Temp - the water temperature of the water sample.
Depth - the salinity of the water sample.
id - an identifier of the survey on which the water sample was taken.
The other variables may be ignored.

Question(s) of interest
The main questions of interest are:

What are the main trends in water quality over this 20 year period?
How do these trends differ at different sampling stations and at different times of year?
What is the influence of temperature and salinity?
Relevant courses
We strongly recommend that you have taken the following courses to undertake this project:

Advanced Predictive Models.
Regression models.

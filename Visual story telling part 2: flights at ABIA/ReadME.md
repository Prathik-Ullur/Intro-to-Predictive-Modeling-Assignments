Consider the data in ABIA.csv, which contains information on every commercial flight in 2008 that either departed from or landed at Austin-Bergstrom Interational Airport. The variable codebook is as follows:

    Year all 2008
    Month 1-12
    DayofMonth 1-31
    DayOfWeek 1 (Monday) - 7 (Sunday)
    DepTime actual departure time (local, hhmm)
    CRSDepTime scheduled departure time (local, hhmm)
    ArrTime actual arrival time (local, hhmm)
    CRSArrTime scheduled arrival time (local, hhmm)
    UniqueCarrier unique carrier code
    FlightNum flight number
    TailNum plane tail number
    ActualElapsedTime in minutes
    CRSElapsedTime in minutes
    AirTime in minutes
    ArrDelay arrival delay, in minutes
    DepDelay departure delay, in minutes
    Origin origin IATA airport code
    Dest destination IATA airport code
    Distance in miles
    TaxiIn taxi in time, in minutes
    TaxiOut taxi out time in minutes
    Cancelled was the flight cancelled?
    CancellationCode reason for cancellation (A = carrier, B = weather, C = NAS, D = security)
    Diverted 1 = yes, 0 = no
    CarrierDelay in minutes
    WeatherDelay in minutes
    NASDelay in minutes
    SecurityDelay in minutes
    LateAircraftDelay in minutes

Your task is to create a figure, or set of related figures, that tell an interesting story about flights into and out of Austin. You can annotate the figure and briefly describe it, but strive to make it as stand-alone as possible. It shouldn't need many, many paragraphs to convey its meaning. Rather, the figure should speak for itself as far as possible.

You have broad freedom to look at any variables you'd like here -- try to find that sweet spot where you're showing genuinely interesting relationships among more than just two variables, but where the resulting figure or set of figures doesn't become overwhelming/confusing. (Faceting/panel plots might be especially useful here.) If you want to try your hand at mapping, you can find coordinates for the airport codes here: https://github.com/datasets/airport-codes. Combine this with a mapping package like ggmap, and you should have lots of possibilities!

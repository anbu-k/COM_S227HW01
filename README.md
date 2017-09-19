# 221HW01
Homework project from "Introduction to Object Oriented Programming" done in Java. See below for assignment description: 

Overview
The purpose of this assignment is to give you some practice with the process of implementing a
class from a specification and testing whether your implementation is correct. None of the code
should be very complicated; most methods are just one line, and the longest one, the visit()
method, can be done in 6 to 8 lines. In particular, you do not need any conditional
statements (i.e. "if" statements) or anything else we haven't covered. You won't be penalized
if you use them, but you'll just be making things more complicated.
For this assignment you will implement two classes, called City and Traveler. The
specification for this assignment includes this pdf along with any "official" clarifications posted
on Piazza. Details are in the next two sections. Here is a brief overview:
A City object just represents a city name along with a cost per night for lodging. There is a
constructor for initializing the city name and lodging cost and there are several accessor
methods. There are no mutator methods. The lodging cost is represented as an integer; the units
are unspecified, but we can think of them as euros.
A Traveler object models a student bumming around Europe, possibly with very little money.
She has a certain amount of money and a current location, represented by a City object. We
assume that she has a rail pass so there is no cost to go from one place to another. (We also do
not consider the need to eat in this model!) The basic operation is to visit a city for a given
number of nights. The name of the city, and the number of nights spent there, are appended to a
string referred to as the "journal". Each city has a certain lodging cost for staying there. If the
traveler doesn't have enough money for lodging, she has to sleep at the train station for some of
those nights. The traveler's funds can be replenished by calling home. However, the traveler's
parents are stuck at home working full time and may not have much sympathy for the traveler
running out of money while gallivanting around Europe. The amount they actually send is
proportional to the number of postcards the traveler has sent to them since the last time she asked
for money. Of course, sending a postcard from a city costs money too. If things are so bad that
the traveler doesn't even have enough money to send a postcard home from her current location,
we say that the traveler is "SOL".


Specification for the City class

There is one public constant:
public static final double RELATIVE_COST_OF_POSTCARD = 0.05;
The cost to mail a postcard from a city is this fraction times the city's lodging cost
(rounded to the nearest integer).

There is one public constructor:
public City(String givenName, int givenLodgingCost)
Constructs a new City with the given name and lodging cost per night.

There are the following public methods:
public String getName()
Returns this city's name.
public int lodgingCost()
Returns this city's lodging cost per night.
public int costToSendPostcard()
Returns the cost to send a postcard from this city. The value is a percentage of the
lodging cost specified by the constant RELATIVE_COST_OF_POSTCARD,
rounded to the nearest integer.
public int maxLengthOfStay(int funds)
Returns the number of nights of lodging in this city that a traveler could afford
with the given amount of money.
public int maxNumberOfPostcards(int funds)
Returns the number of postcards that a traveler could afford to send from this city
with the given amount of money.


Specification for the Traveler class

There is one public constant:
public static final int SYMPATHY_FACTOR = 30;
Proportionality constant when calling home for more money: the amount of
money received is this constant times the number of postcards the traveler has
sent home (since the last time she called home for money).

There is one public constructor:
public Traveler(int initialFunds, City initialCity)
Constructs a traveler starting out with the given amount of money in the given
city. The journal is initially a string consisting of "cityname(start)", where
cityname is the name of the starting city.

There are the following public methods:
public String getCurrentCity()
Returns the name of the traveler's current city.
public int getCurrentFunds()
Returns the amount of money the traveler currently has.
public String getJournal()
Returns the traveler's journal. The journal is a string of comma-separated values
of the form cityname(number_of_nights) containing the cities visited by the
traveler, in the order visited, along with the number of nights spent in each. The
first value always has the form cityname(start) for the starting city. For example,
if a traveler starts in Paris, spends 5 nights in Rome, and then spends 2 nights in
Prague, the journal string would be: Paris(start),Rome(5),Prague(2)
public boolean isSOL()
Returns true if the traveler does not have enough money to send a postcard from
the current city.
public int getTotalNightsInTrainStation()
Returns the number of nights the traveler has spent in a train station when visting
a city without enough money for lodging.
public void visit(City c, int numNights)
Simulates a visit by this traveler to the given city for the given number of nights.
The traveler's funds are reduced based on the number of nights of lodging
purchased. When the funds are not sufficient for numNights nights of lodging in
the city, the number of nights spent in the train station is updated accordingly. The
journal is updated by appending a comma, the city name, and the number of
nights in parentheses.
public void sendPostcardsHome(int howMany)
Sends the given number of postcards, if possible, reducing the traveler's funds
appropriately and increasing the count of postcards sent. If there is not enough
money, sends as many postcards as possible without allowing the funds to go
below zero.
public void callHomeForMoney()
Increases the traveler's funds by an amount equal to SYMPATHY_FACTOR
times the number of postcards sent since the last call to this method, and resets the
count of the number of postcards sent back to zero.

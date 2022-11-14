## Personal planer ++ (notion-like ish) 📝
- o bază de date cu notițele tale
- to do lists
- calendar API
- settings for my account
- light dark theme
- google calendar API ?????
- multiple users that can use the same spaces
- timer stil pomodoro
- support for markdown
- need to figure out synchronization of data si sa vedem ce am salva in databases. We can use [Realm by MongoDB](https://www.mongodb.com/docs/realm/) for example

---

## Bike Pick-up App 🚲

### Chestii in plus pe langa cluj bike:

- dai un rating de safety la bicicleta (actually useful 🤕) ca sa stii ce bicicleta sa alegi
- get a recommendation on which stations to use depending on the desired route (nu stiu exact cum s-ar implementa dar suna cool 😅)

### General features
- Cluj-bike-like
- have a map with pick-up points and status of the stations
- self check-in to pick up the bikes (use qr code or something)
- have a personal account. Gain bonus points that offer discounts /badges/...
- save the history of trips
- solve the situation where more users want to pick up the same bike
- FAQ and report issues
- give a rating of the bike conditions
- every bike should be associated a safety rating that is 
- needs to be mobile friendly

### Ideas:
- tabs:
	- check the status of stations
	- pick up a bike
	- leave the bike
- logic: when we specify our route
- for a station:
	- print nr of bikes available
	- nr of free slots available

## Status:
- shared number of bikes
- multiple users
- fixed stations

## Use cases

0. Get into the account / sign in
	- if not having an account create one
		- the user needs to input a unique username
		- password complexity check (1 nr, bla bla)
		- create the account
	- if having an account, log in

1. Simple bike trip from station A to station B
	- check the number of bikes in station A
	- check if there is any left place in station B

- go to `pick up a bike` section and input to form:
	1. Bike code (automatically check the home station of the bike)
	2. station B (to check if there are any slots left, but we don't save the seat)
- hit the submit button
	- the bike is removed from the station
	- the user session begins (maybe save it in a database of current trips)
- finish the ride:
	- input the destination station (code maybe generated uniquely)
	- get a small form to evaluate the condition of the bike (brakes, ...) then get a score and decide to leave or not the bike into the system

2. The user reaaally wants to take a bike from a station
	- add station to wanted list and get notification when another user leaves a bike there

3. The user tries to pick up a bike that was removed from the available bikes list
	- they get a promt that the bike having the input code is unavailable

4. You are having a session that is too long
	- get several alerts and finally a fine 💰

5. The user wants to get the best bike from the station
	- they click on the button corresponding to the desired station and get the code of the best bike

### Other use cases:
- create new account
- login use case
- delete history of bike rides
- access FAQ
- live support de la un chat bot (reach an answer by successively selecting options offered in chat)
- offer rewards based on biker history


> [!question] Questions
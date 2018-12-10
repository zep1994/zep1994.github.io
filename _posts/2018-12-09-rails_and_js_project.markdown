---
layout: post
title:      "Rails and JS Project"
date:       2018-12-10 00:39:35 +0000
permalink:  rails_and_js_project
---


This project was the most fun for me, because I had a lot of fun working with debugger and well I found A LOT more documentation on JS than Rails. I could type in my problem and easily find a solution to it. This made understanding whats going on a lot easier. I saw one blog that ulitized debugger on just about everything. Anyway for this blog I thought I would talk about the index page. 

First, I set up a class construct with the attributes for one of my models called players. Players on had three attributes and I learned that you can make things easier to read by doing something like this:
```
class Player {
  constructor(attr){
    this.name = attr.name
    this.specialty = attr.specialty
    this.leader = attr.leader
     }
	}
```
Here you can see attr is the arugment and I can say this.id = attr.name. Now is this construct I added a render player function so that everytime a player was created to be shown it would render on the page in an a tag with the players name. 

Next,  I created an empty array to hold all of the players that would be rendered on the page. 
Now, here is the meat of the script. function showPlayers(). This starts by grabbing the area in which the players will be rendered. Otherwise it would try rendering these players and be like "Umm, where?" So moving on with the place we know the players are going. We need to place them in a type of list. To do this. I just did 
```
const playerUL = document.querySelector("ul"). 
```
Great! so now we have an unorderedlist just waiting on those players. Well not just yet. We may have the list, but if you going to do this you need to set the attributes which in this case is just id and the name of the const containing the list area. So we get something like this:
```
playerUL.setAttribute('id', 'playerList')
```
Next, lets just place a h3 inside of player list to show that the data being returned is a bunch of players.
Then we can just appendChild(playerUL) to the playerList const. 

So now we are in a good spot to move on the ajax portion of this. First, we just start a new XMLHttpRequest. I then place the empty allPlayers array into here. Now we need to open the request. This will include GET and the /players url. Now we will get the players URL, but it does not know that this is json. So we tell it that the ResponseType is 'json' and then just send(). Ok, this is a lot, but we are not quite done. We need an onLoad which will be set equal to a function. This function will itterate over each request response and use another function with an argument. We will use this argument to create a new player. Here use that player and push the player to that empty array we created earlier. So now that our array has some players in it, lets create an li to place them in. Aweosome, now it is time to render the players in an a tag. Then we just append the li to the ul. That should now render all of the players. 

Phew! That was a lot. I think it is break time, but I will be back to write about the next project. 

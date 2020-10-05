# Project 2 Notes

Possible data source: https://www.ultimatetennisstatistics.com/about

Location of raw data: https://github.com/JeffSackmann/tennis_atp

Another place: teniisabstract.com


I will likely have to use selenium to access ultimatetennisstatistics



I think imdb.com prevents programmatic searches:

https://www.themoviedb.org/tv/60554

https://www.imdb.com/search/title/?title_type=feature&release_date=1980-01-01,1989-12-31&user_rating=5.1,10.0


Something maybe that helps figuring out how to scrape IMDB:

https://www.dataquest.io/blog/web-scraping-beautifulsoup/



## Algorithm to talk to IMDB
Here it is in pseudo code:


```

number_of_searches = X
search_url = _initial_url_
IMDB_ROOT_URL = "https://www.imdb.com"

list_of_movie_objects = []
first_50 = 0

#this loop runs searches on IMDB
#per search_url
#get's the direct link to the movie
#creates an object of class Movie
#puts the direct link into the object
#saves the object to a pickle

for(i = 0; i < number_of_searches;i++) {

	wait()
	web_response = request(search_url)
	web_response_text = web_response.text
	
	web_response_soup = beautifulsoup(web_response_text)
	
	listOfListerItemContentDIV = web_response_soup.find_all("div", class_="lister-item-content")

	for ListerItemContentDIV in 	listOfListerItemContentDIV {
	
		#relies on knowledge of the structure of the web page
		#hopefully they don't change it lot
		
		link_to_movie = ListerItemContentDIV.h3.a.get("href")
		name_of_the_move = ListerItemContentDIV.h3.a.text
		
		#Should I create an object or just put it in a hash?
		
		#create an object
		#put the object in a list
		
		#why use a class?
		#I can populate the data of each obj of the class with a method call
		#I can make generating the data frame as easy as running a common method
		#on all objects
		
		#Why not use a class
		#have to write more code
		#maybe don't do that now wait until I have
		#a data structure -- but that could cause tech debt maybe better use more
		#robot methodology upfront so you can run faster later
		
		mymovie = Movie(name_of_the_move,link_to_movie)
		
		#list_of_movie_objects.append(mymovie)
		pickle.dump(mymove,MY_PICKLE_FILE)
		

	}
	
	#Found all (moviename,link tuples)
	# that are in page.
	# Save this to a pkl file (first time write, second time append)
	
	
	##TODO How to append to a pickle file
}

```

--> Swap DomesticGross with something else

--> Swap out Title 

--> Names of casts categorical.One-hot-encode category
Encode genre - one-hot-encode

statistical consideration one hot encoding: It you just enumerate categorical things with a number, you will be baking in meaning to the feature that does not exist.

For example if with movies you are dealing with _commedies_,_dramas_,_scifi_,_action_,_horror_ if you labeling them like this:

A single `genre` variable will be encoded like this:

* _comedies_: 1
* _dramas_: 2
* _scifi_: 3
* _action_: 4
* _horror_: 5

Then it would be part of a linear model like this:

```

y = c1 * x1 + c2 * x2 + ... + c\_genre * x\_genre + ... + cN * xN

```

In this case a _horror_ movie will have 6x as  much impact on the final y than a _comedy_ baked into the equation, that the data does not say exists.

So you should one-hot encode categorical data so that each category is a **separate** variable that takes a value of either 1 or 0.

So the equation will look something like this


```

y = c1 * x1 + c2 * x2 + ... + c\_comedy * x\_comedy +  + c\_drama * x\_drama + c\_scifi * x\_scifi + c\_action * x\_action + c\_horror * x\_horror + ... + cN * xN


```

**Downside** to one-hot encoding: If you one-hot encode and add 1000000 features you may have a dimensionality issue (curse of dimensionality), which would require 2^N rows of data for every N feature you add to the regression.



Do EDA on a small dataset with small features to pipe clean

Multi-co-linearity


## Hypothesis

I hypothesize that the cast (especially the director, and the first three actors listed as "Stars" on IMDB) have a large influence on the star rating of a movie.

What I plan to do is list the names of all directors that either won the Oscar Award for Best Director or who directed a film that won Documentary Feature, Best International Feature Film. Justification: See this link

* https://www.latimes.com/entertainment/movies/moviesnow/la-et-en-oscars-2013-nomination-list-story.html
* https://en.wikipedia.org/wiki/Academy_Award_for_Best_Documentary_Feature
* https://en.wikipedia.org/wiki/Academy_Award_for_Best_International_Feature_Film



I omit directors of movies that won Best Picture as this award is given to the producers of said film. So ostensibly the director has no influence on the likelihood of a movie getting this award and thus would not influence the star rating (assuming a movie with high star rating would tend to win Best Picture.)

I omit Best Adapted Screenplay and Best Original screenplay as it is awarded to the writer, who adapts a story from some other medium (like a novel) to a movie screen play. There is evidence that the winner of this award may also serve as the director (_Lord of the Rings_), but it's not know how common that is or whether it's statistically significant. It's outside of the bounds of this study.

I include Best International Feature Film because traditionally the director accepts this award on behalf of his/or film. There is some evidence that the director of a film influences the likelihood of this award, and there are a few directors who are repeat recipients of this award. There is very little data to show that someone who wins this award also will win other awards (_Parasite_ being the only example in history).

Support:

* https://en.wikipedia.org/wiki/Academy_Award_for_Best_Original_Screenplay
* https://en.wikipedia.org/wiki/Academy_Award_for_Best_Picture
* https://en.wikipedia.org/wiki/Academy_Award_for_Best_Adapted_Screenplay


## Mising data notes

I scraped 2000 movies that were reported by IMDB to have been released in 2013.

1479/2000 movies reported domestic gross of $0. That's too much to do any kind of interploation to replace the 0 with some meaningful number.

Going to check 10 random entries to figure out what's going on:

### Movie The Frozen Ground	http://www.imdb.com/title/tt2005374/	

Not domestic gross was listed. Just worldwide gross. Clicking through didn't yield anything


### Shrek the Musical	http://www.imdb.com/title/tt3070936/

No number listed

### Queen	http://www.imdb.com/title/tt3322420/	

No domestic gross just worldwide gross. It's a foreign film so domestic may not be meaningful if it's different countries

### Open Grave	http://www.imdb.com/title/tt2071550/	

No domestic gross just worldwide gross. It's a small number.


### Welcome to the Jungle	http://www.imdb.com/title/tt2193265/	

No Number listed. Relatively low budget film

### http://www.imdb.com/title/tt3720788/	

No number listed. Low budget film

### Hope	http://www.imdb.com/title/tt3153634/	

Nothing reported


### Devil's Knot	http://www.imdb.com/title/tt0804463/

Only worldwide gross listed

### Hawaii	http://www.imdb.com/title/tt2801746/	

Nothing listed

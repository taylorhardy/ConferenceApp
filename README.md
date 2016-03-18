App Engine application for the Udacity training course.
## Conference Organization app
- The conference organization app was built using highly scalable endpoints provided by Googles App Engine. With this app users can register with the app using their google account and create events and mark as attending. Sessions can be also be deleted and all be displayed 

## Task 1: Add Sessions to a Conference
- Endpoints: createSession(if the selected conference exists, adds a session to it), getConferenceSessions(of the given conference, retreives the sessions belonging to it), getConferenceSessionsByType(of a conference and type, returns the list of sessions that meet those criteria), getSessionsBySpeaker(returns all sessions that the speaker is apart of)

- In the way this was setup the conference is the ancestor, so that sessions could be queried by the conference. This made it easier to implement the queries to return the sessions.

- I assumed from previous conferences I've attended that a session could have more than one type, so multiple types are able to be assigned. I believed this would be more realistic

- As for the speakers they are just belong to the session so that the queries can grab data about the session by the speaker or vice versa. 

## Task 2: Session Wishlist
- With this users are able to add sessions to their wishlist, view their wishlist and also remove items. 

## Task 3: Additional Queries/ Query Problem
- For the individuals that like to have the most up to date info, I figured that it would be useful to have a query to return sessions that all of the information had yet to be decided, assuming that this was due to it being new. I also added a query to show sessions today or newer, because the average user doesnt need to know about past sessions. For this I just filtered on session.date using >= date.now().
- As a challenge query we were asked to return all workshop types before 7pm. This was quite tricky as using nbd only allows for one of the comparisions needed, otherwise an error was throw. So since i was able to query on one item I used that to return the sessions before 7pm and then put them in a list by session types so i could grab just the workshop items from that. 
## Task 4: Featured Speaker
- This one I solved for by checking to see if the list of speakers were greater than 1 then store it to the memcache, however, they asked for the app engines task queue to handle adding the Memcache entry. So to do that i just checked if the list of speakers was greater than 1 and used taskqueue.add() per the task queu documentation 

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool
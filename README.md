# JukeBox.li

Jukebox.li is a music jukebox based on Spotify. With Jukebox.li, all 30 million songs on Spotify are available to you and your friends. Create a new room or join an existing one. Together you decide what's going to play next.

This is a personal project of mine. The project is not meant to be used in a production environment.

## Functionality
To use Jukebox.li you need a Spotify account (Premium to listen to the songs).

Currently the following functionalities are available to the user:
- Creating a playlist
- Joining a playlist
- Deleting a playlist (if owner)
- Adding songs to a playlist
- Deleting songs from a playlist (if the user who added the song)
- Upvoting a song to increase probability of playing next
- Listen to current song (premium account needed)


## Architecture
The architecture is split into a frontend and a backend which consist of two separate repositories.

Frontend repo:
Backend repo:

### Frontend
The frontend is an angular application.

It's responsible to communicate and fetch necessary information from the backend as well as the Spotify API.

The frontend handles all calls to the Spotify API with an exception of acquiring the valid Bearer token. This has to be done from the backend as we don't want to expose our Spotify API Secret. We receive the code which we send to our backend, the backend exchanges this code for a valid Bearer token and returns the token to the client.

### Backend
The backend is a Django REST framework instance. It also acts as a Websocket server which is integrated in Django with Django channels.

The backend acts as a RESTful API. Handles user authentication, CRUD-operations on different models. Most importantly it handles the state the current playlist is in (playing song, current time).

## Open Tasks
There is still a lot of room for improvement. Here are the current open tasks, feel free to propose additional ones.

- [ ] Backend authentication, currently a call to the backend needs no authentication. This means everybody can delete playlists, songs etc.
- [ ] Make it possible to hide the username in a playlist - anonymous user
- [ ] Implement topic rooms, e.g electrical music, country etc.
- [ ] Skipping a song that is currently playing
- [ ] Downvoting a song
- [ ] Remove a vote
- [ ] Token renewal, currently the token expires after 10 minutes and a re-login is needed
- [ ] Improve the checking of the current state of the playlist.
- [ ] Improve design

## Creating your own instance

1. Create your own Spotify API project on https://developer.spotify.com/ and get your unique Client ID and Client Secret.

2. Edit the file views.py in the backend and insert your Client ID, Client Secret and your Redirect URL (IP of your frontend, for local development "127.0.0.1:4200") at the top of the file.

3. In the frontend edit the file environment.ts and insert your Client ID, Redirect URI (same as before) and your Backend_IP (IP of backend, again local development 127.0.0.1:8000)

4. Install Docker. Open your terminal and run "docker run -p 6379:6379 -d redis:2.8"

5. Now start the Angular and the Django application.

## Contribution
If you want to contribute, feel free to open a pull request. If possible include any of the task mentioned above. For questions, open an issue or shoot me an email at silas.stulz@gmail.com

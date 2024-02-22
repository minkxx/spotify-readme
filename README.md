<div align="center">
  <img src="assets/spotify.svg" width="100" align="center">
  <h1>Spotify Readme</h1>

  [![Badge](https://img.shields.io/github/issues/minkxx/spotify-readme?style=for-the-badge)](https://github.com/minkxx/spotify-readme/issues)
  [![Badge](https://img.shields.io/github/forks/minkxx/spotify-readme?style=for-the-badge)](https://github.com/minkxx/spotify-readme/network)
  [![Badge](https://img.shields.io/github/stars/minkxx/spotify-readme?style=for-the-badge)](https://github.com/minkxx/spotify-readme/stargazers)

</div>

<p align="center">
  A dynamic, customizable, and real-time Spotify now-playing widget for your README files that syncs with the song you’re currently playing. If you're not currently playing a song, it'll display one of your recent songs! Feel free to ask for help or make any PRs/issues/suggestions 😄
</p>

## Previews

#### Default
```
/
```
![Preview](https://minkxx-spotify-readme.onrender.com)

#### Spinning CD Effect
```
/?spin=true
```
![Preview](https://minkxx-spotify-readme.onrender.com/?spin=true)

#### Include Scan Code
```
/?scan=true
```
![Preview](https://minkxx-spotify-readme.onrender.com/?scan=true)

#### Rainbow Equalizer
```
/?rainbow=true
```
![Preview](https://minkxx-spotify-readme.onrender.com/?rainbow=true)

#### Dark Theme
```
/?theme=dark
```
![Preview](https://minkxx-spotify-readme.onrender.com/?theme=dark)

## Setup/Deployment

#### 1. Spotify's API

* Head over to the <a href="https://developer.spotify.com/dashboard/">Spotify developer portal</a>.
  * Create a Spotify application.
    * In the **App name** & **App description** fields, you may put whatever you want.
    * Agree with Spotify's TOS and click **Create**.
  * Take note of the **Client ID** & **Client Secret**.
  * Click **Edit Settings**.
    * Add `http://localhost/callback/` to **Redirect URIs**.

#### 2. Intermediary Steps

```
https://accounts.spotify.com/authorize?client_id={CLIENT_ID}&response_type=code&scope=user-read-currently-playing,user-read-recently-played&redirect_uri=http://localhost/callback/
```

* Copy and paste the above link into your browser.
  * Replace `{CLIENT_ID}` with the **Client ID** you got from your Spotify application.
  * Vist the URL.
    * Log in if you're not already signed in.
    * Click **Agree**.
* After you get redirected to a blank page, retrieve the URL from your browser's URL bar. It should be in the following format: `http://localhost/callback/?code={CODE}`.
  * Take note of the `{CODE}` portion of the URL.
* Head over to <a href="https://base64.io">base64.io</a>.
  * Create a string in the form of `{CLIENT_ID}:{CLIENT_SECRET}` and encode it to base 64.
  * Take note of the encoded base 64 string.
* If you're on Windows or don't have the `curl` command, head over to <a href="https://httpie.io/cli/run">httpie.io/cli/run</a>.
  * Press enter.
  * Clear the pre-filled command.
* If you're on Linux or Mac with the `curl` command, open up your preferred terminal.
* Run the following command (replace `{BASE_64}` and `{CODE}` with their respective values):

  ```bash
  curl \
    -X POST \
    -H "Content-Type: application/x-www-form-urlencoded" \
    -H "Authorization: Basic {BASE_64}" \
    -d "grant_type=authorization_code&redirect_uri=http://localhost/callback/&code={CODE}" \
    https://accounts.spotify.com/api/token
  ```

* If you did everything correctly, you should get a response in the form of a JSON object.
  * Take note of the `refresh_token`'s value.

#### 3. Host on Render

* Fork this repository.
* Head over to <a href="https://render.com">Render</a> and create an account if you don't already have one.
  * Add a new web service on Render.
    * Link your GitHub account if you haven't done so already.
    * Make sure Render has access to the forked respository.
    * Import the forked respository into your project.
      * Give it a meaningful name.
      * Keep the default options for the other settings.
      * Add the following environment variables along with their appropriate values:
        * `CLIENT_ID`
        * `CLIENT_SECRET`
        * `REFRESH_TOKEN`
      * Click **Create Webservice**.
      * Click **Continue to Dashboard**.
        * Find the **Domains** field and take note of the URL.
          * Example: `{NAME}.onrender.com`.
         
#### 4. Host on Render

* Fork this repository.
* Head over to <a href="https://vercel.com">Vercel</a> and create an account if you don't already have one.
  * Add a new project.
    * Link your GitHub account if you haven't done so already.
    * Make sure Vercel has access to the forked respository.
    * Import the forked respository into your project.
      * Give it a meaningful name.
      * Keep the default options for the other settings.
      * Add the following environment variables along with their appropriate values:
        * `CLIENT_ID`
        * `CLIENT_SECRET`
        * `REFRESH_TOKEN`
      * Click **Deploy**.
      * Click **Continue to Dashboard**.
        * Find the **Domains** field and take note of the URL.
          * Example: `{NAME}.vercel.app`.

#### 5. Add to your GitHub

* In any markdown file, add the following (replace `{PROJECT_NAME}` with the name you gave your Render project):

  ```html
  <a href="https://github.com/minkxx/spotify-readme">
    <img src="https://minkxx-spotify-readme.onrender.com/" alt="Current Spotify Song">
  </a>
  ```

* Please leave the anchor tag hyperlink reference to this GitHub repo to retain creator credit and for other users to find! 


## Note

This repo is a forked version of <a href="https://github.com/xditya/Spotify-Readme-New">Xditya's forked project project</a> from <a href="https://github.com/tthn0/Spotify-Readme">tthn0's project project</a>. I just made this repo deployable on <a href="https://render.com">Render</a>

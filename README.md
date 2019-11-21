# Tweeter

The goal of this project was to test out the use of jQuery for HTTP requests.

## 1. Import jquery into the program

Copy the jquery.min.js file into the same folder as the main html document (index.html). 

Include this script tag in the body of index.html:
```Javascript
<script src="jquery.min.js" type="text/javascript"></script>
```

## 2. Handle CORS

In config/application.rb, within the Application class, add the following:

```Ruby
config.action_dispatch.default_headers = {
    'Access-Control-Allow-Origin' => '*'
}
```

## 3. Write the get request

Add a button to index.html, which can be used to call the function. This is not completely necessary because the function can be called on load.

```
<button>Get tweets</button>
```

Add the script to make the button call the function:
```
document.querySelector("button").addEventListener("click", getTweets);

function getTweets() {
    $.get("http://localhost:3000/tweets.json", (response) => {
        console.log(response);
        let output = '';
        response.forEach((tweet) => {
            output += `<li>${tweet.message}</li>`;
        });

    tweetHolder.innerHTML = output;

    });
}
```

## 4. Render the output to HTML instead of console

The DOM is used to inject HTML into the document. First we create a div and give it an id, which will be used to reference the div to inject HTML later.

We use the id of the div with a dot notation 'innerHTML' to inject a variable into the div.

```
tweetHolder.innerHTML = output;
```
## 5. Implement fetch

Fetch is an alternative to jQuery, which is built directly into javascript.

Firstly declare the getTweets function as asynchronous.
```
async function getTweets()
```

Then create the myJson object, which will hold the JSON response from the API.
```
const response = await fetch("http://localhost:3000/tweets.json");
const myJson = await response.json();
```

Then iterate through the myJson object and extract the messages, save them under a variable called output, and inject the output variable into the HTML document.
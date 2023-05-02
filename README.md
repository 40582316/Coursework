# Coursework
Created with CodeSandbox
Static HTML/JS/CSS website with dynamically loaded content using external API
The website was created as a requirement for Web Technologies unit.

Disclaimer
The website shouldn't be considered as a finished product. And as it is allowed to copy it - it shouldn't be used in the production environment.

Defined requirements
API loaded content
Food related
Hosted on static Github pages
Technology overview
###external (not required add on) The website uses Edamam API to retrieve content based on visitor search requests or in response to clicking on predefined in the button API request. Edamam API requires registration and free access has a limited number of requests over time. 10 requests a minute it seems generous as long as the number of users is very limited ( 1 digit number) Still good enough for development purposes. Because it requires registration it seemed to be a good idea to create some proxy for the API and requests to avoid disclosure of the API key and id. On the static website, there is no way to hide the request, and the request requires to append key and id. Another solution would be to obfuscate the request or even use some encoding (ie.:base64, etc), although it wouldn't be the best as it will only require a bit more effort to find the 'secrets' for someone willing to abuse the opportunity. Also Proxy could introduce its own limits and cache. This solution would prevent reaching limits on Edamam - the API provider. The Proxy was created on codesandbox.io Relatively simple serverless function using Node.js. The code for this solution was heavily inspired by Traversy Media's "weather project", a YouTube tutorial.

HTML
The website is split into a few subpages based on narrowed subjects. Depending on the user's interest one can navigate to the page of interest. Although initially considered to make it all as one page, app-like, depending on the purpose of the page, redirecting to subpages could keep the user's attention for longer, allowing to display of more promoted content or affiliate links. Although it would be recommended to attach some analytics script( Google Analytics) to follow visitors' behaviour and adjust based on that insight. The page could be relatively easily merged into one page and be deployed as a single-page web app. Nothing out of the ordinary was used. Although <section> element in place just to keep the code tidy. Considerations for future development: metatags: ie.: <meta property="og:type" content="website">(for SEO); <aria> elements (for visually impaired users) - but not limited to.
There are already in place social media icons, but they are only placeholders. The functionality is not implemented not required at this stage.

CSS
It includes media queries for different resolutions screens.

@media (max-width: 420px) {
 .search-result {
   grid-template-columns: 1fr;
   /* display: block; */
 }
}
Not tested extensively but it worked on different sizes of windows on Windows operating systems (Chrome, Edge, Firefox) and on Chrome on Android phones. Also used keyframes to add visual effects to the main title on the page, which is also a link to the main page on subpages:


@keyframes text_reveal {
  100% {
    color: whitesmoke;
  }
}
The CSS is split into multiple files - which is not optimal for production, but it was considered convenient for development. - Easier to find a required property and easier to debug. It has to be merged into one file to reduce the number of requests to the server - which is important to reduce loading time. It also wasn't checked for possible(very) duplicates.

JavaScript
JavaScript is responsible for the functionality of the website. It allows for the interaction of the user with the page. The content is dynamically loaded in response to user actions. There could be by typing in the input field or clicking on one of the multiple buttons with points of interest for the user. No JavaScript was used to adjust the user interface or any other visual aspects of the website. It was considered for its simplicity and to avoid any potential compatibility issues with other browsers. CSS used was more than enough - with that in mind the visual aspect wasn't the priority.

Funcionality detail
The main url for the query is "https://wjk69x-5000.csb.app/api?q=" as an entry point for the API proxy serverless function on codesandbox.io. In the recipe.html - where the visitor can search for the recipe based on the dish name, the form contains the text input field. see below:

      <form>
        <input type="text" placeholder="Search Your Recipe...">
        <ion-icon name="search"></ion-icon>
        <br>
        <input id="button0" type="submit" value="Search">
      </form>
Typed text is retrieved as value by JavaScript(app0.js) and appended to the URL to create the request. The search query is not validated and it can return an empty response if no item is found - but this is on Edamam's side.

let searchQuery = "";
let btn = document.querySelectorAll(".btn");
for (i of btn) {
  i.addEventListener("click", function (e) {
    searchQuery = this.value;
    e.preventDefault();
    
    
e.preventDefault(); removes unwanted browser behaviour like jumping, and trying to reload the page after clicking on what is recognised by the browser as a link.

and:

const res = await fetch(url + searchQuery);
"URL" comes from a separate .js file. It was a solution, to streamline the development process, - the URL was changed a few times due to some quirks on codesandbox.io. Another reason - the same parameter is used on diet.js - for searching the recipe based on user input - and by app0.js - where the search is predefined based on parameters provided on Edamam documentation. Files app0.js and diet.js - could be eventually merged later on, as they have been used separately for easier development and debugging. As an example in diet.js the value of the button is predefined: maindish.html

<button type="submit"  class="btn"  id="button0" value="&mealType=snack">Snack</button>
"&mealType=snack" - is based on Edamam documentation, where recipes can be retrieved based on the "mealType" parameter. Another parameter used is: "health=" - for example in vegetarian.html:

<button type="submit"  class="btn"  id="button0" value="&health=vegetarian">vegetarian</button>

Other arguments: "cuisineType="

<button type="submit"  class="btn"  id="button0" value="&cuisineType=caribbean">Caribbean</button>
"diet="

<button type="submit"  class="btn"  id="button0" value="&diet=high-protein">Muscle Mass Building Diet</button>
"health="

<button type="submit"  class="btn"  id="button0" value="&health=paleo">Paleo Diet</button>
Conclusion
The website covers all required aspects. Funcionality and method/ place of deployment, and subject. The visual and UI aspect as it wasn't mentioned in the requirements - was pushed to the second plan - as it is subjective matter of taste anyway. Outside of requirements the layer of security was added in the form of proxy for the API to avoid exposing indyvidually assigned API key and id, and to avoid potential abuse of it. Although the solution hardly can be considered as bulletproof, there could be enough for the limited (visitors/time wise) of the website. There is many points where improvement can be made - some of them have been mentioned in the main body of this description. As the website should by only considered as a rough state of developement, more as proof of concept.
Another thing to consider for the production stage - would be to add pop up with cookies consent, as required by EU GDPR regu;ation. As for now the website itself doesn't use any cookies, but rthere could be some included by the GitHub.

License
To Do (assume public domain unless stated otherwise)

# Coursework
Created with CodeSandbox
Static HTML/JS/CSS website with dynamically loaded content using external API
The website was created as a requirement for Web Technologies unit.

Disclaimer
The website shouldn't be considered as a finished product. And as it is allowet to copy it - it shouldn't be used in the production environment.

Defined requirements
API loaded content
Food related
Hosted on static Github pages
Technology overview
###external (not required add on) The website uses Edamam API to retrieve content based on visitor search request or in response to clicking on predefined in the button API request. Edamam API requires registration and free acces has a limited number of requests over time. 10 requests a minute it seems generous as long as number of users is very limited ( 1 digit number) Still good enough for development purpouse. Becouse it requires the registration it seemed to be a good idea to create some kind of proxy for the API and requests to avoid disclousure of the API key and id. On the static website there is no way to hide the request, and the request requires to append key and id. Other solution would be to obfuscate the request or even use some encoding (ie.:base64, etc), although it wouldn't be the best as it will only require a bit more effort to find the 'secrets' for someone willing to abuse the opportunity. Also Proxy could introduce own limits and cache. This solution would prevent reachng limith on Edamam - the API provider. The Proxy was created on codesandbox.io Relatively simple serverless function using Node.js. The code for this solution was hevily inspired by on Traversy Media "weather project", YouTube tutorial.

HTML
The website is split into few subpages based on narrowed subject. Depends on the user interest one can navigate to the page of interest. Al5though initially wos considered to make it all as one page, app-like, but depends of the porpouse of the page, redirecting to subpages could keep user's attention for longer, alowing to display more promoted content, or afiliate links. Although it would be recomended to attach some analitics script( Google analitics) to follow visitors behaviour and adjust based on that insight. The page could be relatively easy merged into one page and be deloyed as a single page web app. Nothing out of ordinary used. Although <section> element in place just to keep the code tidy. Comsiderations for future developement: metatags: ie.: <meta property="og:type" content="website">(for SEO); <aria> elements (for visually impaired users) - but not limited to.
There are already in place social media icon, but they are only as placeholders. The funcionality is not implemented not required at this stage.

CSS
It includes media queris for different resolutions screens.

@media (max-width: 420px) {
 .search-result {
   grid-template-columns: 1fr;
   /* display: block; */
 }
}
Not testeg extensively but it worked on different sizes of windows on Windows operating systems (Chrome,Edge,Firefox) and on Chrome on Android phones. Also used keyframes to add visual evvect to the main title on the page, which is also a link to the main page on subpages:


@keyframes text_reveal {
  100% {
    color: whitesmoke;
  }
}
The CSS is split in multiple files - which is not optimal for production, but it was considered as convenient for development. - Easier to find required property and easier to debug. It has to be merged into one file to reduce number of requests to the server - which is important to reduce loading time. It also wasn't checked for possible(very) duplicates.

JavaScript
JavaScript is responsible for the funcionality of the website. It allows for interaction of the user with the page. The content is dynamicly loaded in response of use actions. Ther e could by typing in the input field or clicking on the one of multiple buttons with points of interests for the user. No JavaScript was used to adjust user interface, or any other visual aspects of the website. It was considered for the simplicity and to avoid any potencial compatibility issues with other browsers. CSS used was more than enough - with that in mind the visual aspect wasnt the priority.

Funcionality detail
The main url for the query is "https://wjk69x-5000.csb.app/api?q=" as an entry point for the API proxy serverless function on codesandbox.io. In the recipe.html - where the visitor can search for the recipe based on the dish name, the form contains the text input field. see below:

      <form>
        <input type="text" placeholder="Search Your Recipe...">
        <ion-icon name="search"></ion-icon>
        <br>
        <input id="button0" type="submit" value="Search">
      </form>
Typed text is retrieved as value by JavaScript(app0.js) and append to the url to create the request. The search query is not validated and it can return empty response if no item found - but this is on Edamam side.

let searchQuery = "";
let btn = document.querySelectorAll(".btn");
for (i of btn) {
  i.addEventListener("click", function (e) {
    searchQuery = this.value;
    e.preventDefault();
    
    
e.preventDefault(); removes unwanted browser behaviour like jumping, trying to reload the page after clicking on what is recognised by the browser as link.

and:

const res = await fetch(url + searchQuery);
"url" comes from separate .js file. It was a solution, to streamline developement proces, - the url was changed few times due to some quirks on codesandbox.io. Another reason - the same parameter is used on diet.js - for searching the recipe based on user input - and by app0.js - where search is predefined based on parameters provided on Edamam documentation. Files app0.js and diet.js - could be eventually merget later on, as they have been used separately for easier developement and debugging. As an example in diet.js the value of the button is predefined: maindish.html

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

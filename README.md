## Day 31:
- Add routing to your User Creator client app! Each "page" should a be separate bit of logic. Now you no longern eed an App.svelte with if this, display this component, otherwise, display this other component. Each bit of functionality can be separate! Thisis how how we give our front-end apps STRUCTURE, to make code clean and separate.
IE: A Home page, that people land on. A button to get to the REGISTER page, which creates a user. A button to SEE all the users. A button to EDIT your user.
They should all be wrapped by the main "layout" in app.svelte.

Use the svelte-spa-router library here. There are many libraries, I liek this one, feel free to try a different one!
https://github.com/ItalyPaleAle/svelte-spa-router 


## Day30:
x- Add a password, and passowrd hashing via either bcrypt or argon2, to your express user creation route!
x- Add a post /login route a user can use to login, verify the password is correct, and receive a JWT!
x- Add JWT verification to your PUT /user route so only logged in users can edit their own user!
x- add a Login page to your client that stores the JWT to localStorage if the password is correct
- Update the client to use these routes, and for editign the user, get the JWT out of  local storage when they try to update the form, setting it as a Authorization request header in the form: Bearer $token}.
## Day29: Real-world data structuring

# HOMEWORK:
x- Create a new Svelte app with vite,
x-  and a new Express app, and put them in the client and server folders respectively, as we've been doing. 
x-  Use DaisyUI and Tailwind if you like!
x- Create a User model with id, username, and email properties.
x-  Use the uuid npm package to create unique IDs for your models.
x- Add a fireStore (or supabase, whatever database you like to use) config to your project. 
x- Create one svelte form to create a user, with two inputs for username and email.
Create four express handler routes:
x- a /user .post to create a new user, 
???????????????????????????????????????????????????????????????????????
x- a  /user/:id .put which can update the user by ID, 
?????????????????????????????????????????????????????????

x- a .get /user to fetch all users, and 

x- a /user/:id .get to get a user by ID.


x- Create a svelte page (and button to get there) that displays all users in a list. 

x- After clicking a user, you should be taken to a third page which lets you edit that user's 
username or email address via a form, which you can complete because you know the ID of the user from selecting it in the list.

x- Deploy both the client and the server to vercel.

PLEASE CREATE A NEW APP FOR THIS. DONT REUSE OLD ONE. WE WANT TO GET FAMILIAR WITH THIS SETUP OF NEW APPS AND NOT LET IT GET DUSTY!! WE WANT TO BE WRITING NEW EXPRESS HANDLERS AND NEW SVELTE COMPONENTS CONSTANTLY, THIS IS THE WHOLE POINT!
It may seem easy to repurpsoe your Todo List app for this. DONT DO IT! You need to be redeploying this stuff via Vercel, and re-writing these bits to drive them home!

3 days for this homework! Next lesson Thursday night. 
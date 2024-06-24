# Capstone_Project
Link to my google docs: https://docs.google.com/document/d/1KL21_NaI7kRTw9fwu3xiheg8ZHm7uM7ODjQUxsFxfaA/edit?usp=sharing
My Capstone Google Docs and Screen Archetypes

Meta University Eng Project Plan Template     
[Project Name]
Intern: Dara Oyedun
Intern Manager: Ayoub Mansar
Intern Director: Paulina Anzaldo
Peer(s): Samir Hashem, Joel Metcalf
GitHub Repository Link: https://github.com/OluwadaraO/Capstone_Project

Overview
My project is a recipe website that aims to provide users with a personalized cooking experience. It solves the problem of finding and organizing recipes, meal planning, and grocery shopping by offering a user-friendly platform with features such as search filters, meal planning tools, and grocery list integration. The website also fosters a community of cooks by allowing users to share and discover new recipes, rate and review recipes, and interact with other users through comments and forums.
Category: Lifestyle and Utility
Story: a recipe website is a personalized cooking platform that transforms kitchen ingredients into delicious meals. Upon signing up, users answer questions about their dietary preferences, cooking skills, and the ingredients they typically have. This information crafts a tailored dashboard of recipe recommendations.
Market: Homecooks
Habit: This website will be used daily for individuals (homecooks) who rely on the website for daily meal planning and preparation
Scope: I would want users to be able to get recipes based on the ingredients they have.

Product Spec
Recipe Book App Product Specification

1. User Registration and Personalization
Sign-Up/Login: Users can create an account or log in to access personalized features.
Personalization Questions: During sign-up, users answer questions about dietary preferences, allergies, and interest in trying new recipes.
Customized Recipe Display: After sign-up, users are directed to a page displaying recipes tailored to their preferences.

2. User Profiles and Customization
Personalized Recommendations: Algorithms suggest recipes based on users' dietary preferences, past selections, and available ingredients.
Profile Management: Users can update their dietary preferences, skill level, and other personal details to refine recipe suggestions.

3. Search and Filtering Capabilities
Advanced Search Options: Implement a robust search function that allows users to find recipes based on ingredients, cooking time, dietary restrictions, and other criteria.
Dynamic Filtering: Enable users to filter recipes easily by categories such as meal type, cuisine, or popularity.

4. Recipe Discovery and Management
Ingredient-Based Search: Users can input available ingredients via a pop-up form to find matching recipes.
Detailed Recipe Information: Each recipe includes details such as ingredients, preparation steps, and nutritional information like calorie content.
Recipe Filtering: Recipes can be searched and filtered based on ratings, calorie count, popularity, and more.

5. Community Interaction
Comments Section: Users can discuss recipes, share tips, and ask questions in a community comments section under each recipe.
Likes: Users can like recipes, helping to highlight popular choices within the community.

6. Interactive Features
Rating and Reviews: Users can rate recipes and leave feedback, enhancing decision-making for others and improving recipe quality.
Recipe Submission: Users can submit their own recipes, contributing to the diversity of available recipes and fostering community engagement.

7. Meal Planning Tools
Weekly Meal Planner: The app provides a tool for users to plan their weekly meals, which also generates a shopping list based on selected recipes.
Grocery List Integration: Users can create and customize grocery lists directly from the recipes, facilitating easy shopping preparation.

User Stories
Required
User can register for an account to personalize and save dietary preferences
User can log in to access personalized dashboard and saved recipes
User can answer questions about dietary preferences and allergies during sign up process to receive tailored recipe suggestions
User can update profile to adjust dietary preferences and cooking skill
User can search for recipes based on specific ingredients at home
User can filter recipes by meal type, cuisines or popularity 
User can see detailed information about each recipe including ingredients, cooking steps and nutritional information
User can rate and review recipes to share experience and improve recipe recommendations
User can plan meals for the week using a meal planner tool
User can generate and customize a grocery list based on selected recipes
User can ask in the comment section for cooking tips and recipes
User can like recipes and add to favorites
User can receive personalized recipe recommendations based on past selections and current ingredient availability to discover new favorites

Optional
Users can submit recipes (fetching from two places api and database. Could have a button like recipes curated by users and when they click on it it should fetch data from the database)
User can customize the user interface with themes/color schemes
User can receive ingredient substitution suggestions if missing an ingredient
User can have a feature called “surprise me” that randomly selects a recipe based on the users’ preferences
Screen Archetypes


Data Model
https://excalidraw.com/#json=GTJ94Defak6iSxxTA5vep,RDFU2gXYB1hewWbtUqkkaA


Users:
ID: Integer UUID (Unique identifier for each user) 
Username: String (Chosen username of the user)
Password: String (Encrypted password using bcrypt)
Profile Picture: String (URL to the user's profile picture)
Dietary Preferences: Array (String) (List of dietary restrictions or preferences, e.g., "gluten-free", "vegan")
Allergies: Array (String) (List of allergies, e.g., "nuts", "dairy")
Liked Recipes: Array (UUID) (Foreign Key referencing recipes liked by the user)

Recipes:
ID: Integer UUID (Unique identifier for each recipe)
Title: String (Title of the recipe)
Description: String (Brief description of the recipe)
Ingredients: Array Object(List of ingredients, each object containing ingredient name and quantity)
Instructions: Array String (Step-by-step cooking instructions)
Image URL: String (URL to an image of the finished dish)
Nutritional Information: Object (Details such as calories, fat content, protein, etc.)
Category: String (Type of meal, e.g., "breakfast", "lunch", "dinner")
Cuisine: String (Cuisine type, e.g., "Italian", "Mexican")
Rating: Float (Average rating based on user reviews)

Comments:
ID: Integer UUID (Unique identifier for each comment)
Recipe ID: UUID (Foreign Key referencing the recipe commented on)
Author ID: UUID (Foreign Key referencing the user who made the comment)
Content: String (Text content of the comment)
Timestamp: DateTime (Date and time the comment was posted)

Ratings:
ID: Integer UUID (Unique identifier for each rating)
Recipe ID: UUID (Foreign Key referencing the recipe rated)
User ID: UUID (Foreign Key referencing the user who rated the recipe)
Score: Integer (Rating score, typically on a scale of 1 to 5)




Server Endpoints
1. User Authentication

POST /signup(Create new account)
  Body Parameters: username, username, password, dietary_preferences, allergies
POST /login (User login)
POST /logout (User logout)
  No parameters required
2. User Features

GET /users/{id} (Retrieve user profile)
   Path Parameter: id (user ID)
PUT /users/{id} (Update user profile)
  Path Parameter: id (user ID)
   Body Parameters: updated_profile_data
GET /users/{id}/favorites(Retrieve user's favorite recipes)
   Path Parameter: id (user ID)

3. Recipe Management

GET /recipes(Retrieve all recipes)
  Query Parameters: filter (e.g., cuisine, meal type), sort (e.g., rating, popularity)
GET /recipes/{id} (Retrieve recipe details)
  Path Parameter: id (recipe ID)
POST /recipes(Create a new recipe)
  Body Parameters: recipe_data
PUT /recipes/{id} (Update a recipe)
  Path Parameter: id (recipe ID)
  Body Parameters: updated_recipe_data
DELETE /recipes/{id} (Delete a recipe)
   Path Parameter: id (recipe ID)

4. Comments and Ratings

GET /recipes/{id}/comments(Retrieve comments for a recipe)
   Path Parameter: id (recipe ID)
POST /recipes/{id}/comments(Post a comment on a recipe)
  Path Parameter: id (recipe ID)
  Body Parameters: comment_data
POST /recipes/{id}/ratings (Rate a recipe)
  Path Parameter: id (recipe ID)
  Body Parameters: rating_score

5. Meal Planning

GET /users/{id}/meal-plans (Retrieve user's meal plans)
   Path Parameter: id (user ID)
POST /users/{id}/meal-plans(Create a new meal plan)
   Path Parameter: id (user ID)
   Body Parameters: meal_plan_data

6. Grocery list planning
GET/users/{id}/grocerylist (Retrieve user’s grocery list)
Path parameter: id(user ID)
	POST/users/{id}/grocerylist (Create a new grocery list)
Path parameter: id(user ID)
Body paramters: ingredents, quanitity

Navigation

Project Requirements
1. Database Interaction
Database Used: PostgreSQL
Functionality: The website will interact with the PostgreSQL database to store and retrieve user data, including profiles, preferences, and user-submitted recipes. This ensures that user information is securely managed and easily accessible.

2. API Integration
API Used: Edamam
Functionality: The website will integrate with the Edamam API to fetch a wide range of recipes, nutritional information, and ingredient details. This integration enhances the user experience by providing extensive, reliable, and up-to-date culinary data.

3. User Authentication
Login/Logout: Users can log in and log out of the website, ensuring that their profiles and preferences are securely accessed and personalized.
Sign Up: New users can sign up, creating a unique user profile where they can set dietary preferences, allergies, and other personal details, which are used to tailor recipe recommendations.

4. Multiple Views
Implementation: The website will feature multiple views, including a home page, recipe detail pages, user profile pages, and meal planning views. Each view serves a specific purpose, enhancing navigation and user interaction.

5. Custom Cursor Interaction
Implementation: The website will include custom tooltips that appear when users hover over certain elements, such as ingredients or tool icons (like a sidebar disappearing when the user is no longer hovering on the icon). These tooltips provide additional information, enhancing the user experience and providing guidance without cluttering the interface.

6. Complex Visual Styling
Implementation: The website will feature a custom-designed recipe card component that displays recipes in a visually appealing manner. This component is styled from scratch and includes elements like image overlays, gradient text backgrounds, and hover animations, showcasing advanced CSS skills.

7. Loading State
Implementation: The website will use a loading state when fetching data from the Edamam API or loading content from the database. This state might include animated loaders or skeleton screens that maintain visual polish and inform users that content is being loaded.



Technical Challenges
For your project, you should demonstrate that you can apply what you’ve learned so far and expand on that knowledge to write code and implement features that go beyond the scope of the projects you worked on during CodePath.

Based on the general idea and direction of your project requirements, your intern manager will create at least two (2) Technical Challenges for you. This section is all about explaining what they are and how you’re planning to tackle them - you’ll work together with your manager to fill it out. 

Technical Challenge #1 -  MACHINE LEARNING FOR PERSONALIZED RECIPE RECOMMENDATIONS
What
Problem Solving: The primary problem being addressed is the customization of recipe recommendations to enhance user satisfaction and engagement. Traditional static recommendation systems may not effectively cater to the unique tastes and dietary preferences of individual users. By implementing a machine learning model, the website can learn from user interactions (such as ratings, likes, and dietary preferences) to dynamically suggest recipes that are more likely to appeal to each user. 

Beyond Basic Learning: This involves training a model on a dataset of recipes and user preferences to predict which recipes a user is most likely to enjoy. The model will take into account factors such as dietary restrictions, ingredient preferences, and cooking skill level. This challenge goes beyond the basic web development skills learned in CodePath by incorporating machine learning algorithms to analyze and predict user preferences.
How
Pseudo Code Idea (Based on what I researched)
// Train model on recipe dataset
model.train(recipes, user_preferences)

// Get user preferences from signup form
user_prefs = get_user_prefs()

// Predict top 5 recipes for user
predicted_recipes = model.predict(user_prefs)

// Display predicted recipes on dashboard
display_recipes(predicted_recipes)
Solution Approach:
Data Collection: Gather user data through interactions and preferences.
Model Training: Use a recommendation algorithm (e.g., collaborative filtering) to train a model based on user data.
Integration: Integrate the model with the backend using Node and Express to serve personalized recipe suggestions.

Technical Challenge #2 - REAL-TIME CHATTING FOR LIVE USER INTERACTION
What
Problem Solving: The challenge addresses the need for real-time interaction among users without reloading the webpage, enhancing the user experience by providing immediate feedback and fostering a sense of community. Traditional methods might involve reloading the page for new comments, which can disrupt the user experience and increase load times.
Beyond Basic Learning: Implementing real-time communication extends beyond what was taught in CodePath. It involves using advanced real-time web technologies, potentially integrating WebSockets or similar technologies for live data transmission.
How
Pseudo Code Online (Based on what I researched)
// Establish WebSocket connection
ws.connect()

// Send message to server
ws.send(message)

// Receive message from server
ws.onmessage = function(event) {
  // Update chat log in real-time
  update_chat_log(event.data)
}
Solution Approach: 
WebSocket Integration: Implement WebSockets to establish a persistent, real-time connection between the client and server.
Server Setup: Configure the server to handle incoming messages and broadcast updates to connected clients.
Client-side Handling: Update the client-side JavaScript to handle incoming WebSocket messages and update the UI accordingly.

Database Integration
PostgreSQL: PostgreSQL is a powerful and free database system that helps you store and manage data efficiently. For my recipe website, PostgreSQL can handle all the data related to users, recipes, ingredients, and comments securely and reliably. It allows users to easily retrieve, update, and manage information and also ensure that everything from user profiles to recipe details is organized and accessible. This makes it an excellent choice for handling the complex data interactions required by a dynamic and interactive recipe website.
External APIs
Edamam API: The Edamam API is a tool that provides access to a vast database of recipes, nutritional information, and food data (which I need for my recipes website). It allows developers to integrate these features into their applications, enabling users to search for recipes based on ingredients, dietary preferences, and more. The API simplifies the process of retrieving detailed food-related information, which can be used to enhance user experience in cooking or health-related apps.

Authentication
User authentication on the recipe website will be managed using a combination of Node.js and Express along with Prisma for interacting with the PostgreSQL database. The process will involve both signing up new users and logging in existing users.
1. Sign Up:
Users will provide essential information such as email, password, dietary preferences, and possibly other personal details during the sign-up process.
The password provided by the user will be hashed using a secure hashing algorithm (bcrypt) before being stored in the database to ensure security.
Upon successful registration, the user will be automatically logged in, and a session will be initiated.
2. Log In
Users will log in using their email and password.
The system will validate the credentials against the stored data in the database.
If the credentials are correct, a session will be created, allowing the user to navigate the protected areas of the website.
3. Cookie / Session Management
To manage sessions, I will use the Express.js session middleware, which provides a simple way to store and retrieve session data.
The session data will be stored in a cookie on the client-side, using the express-session module.
The cookie will contain the session ID, which will be used to authenticate the user for subsequent requests to the server.
To ensure that the session data is secure, I will use HTTPS encryption to protect the communication between the client and server.
4. Navigation Between Screens
To enable seamless navigation between different screens, I will use the Express.js router to define routes for each screen.
Each route will be associated with a specific URL, and will render the appropriate screen when accessed.
To ensure that the user remains authenticated throughout their session, I will use the session middleware to check for the presence of a valid session ID on each request.
If the session ID is valid, the user will be allowed to access the requested screen. If not, they will be redirected to the login screen.
Visuals and Interactions
Interesting Cursor Interaction: My recipe website uses a custom cursor that changes shape and size when hovering over interactive elements, such as buttons and links. This is achieved using CSS and JavaScript to manipulate the cursor's appearance and behavior.

UI Component with Custom Visual Styling: The website features a custom-designed recipe card component that displays recipes in a visually appealing manner. This component is styled using CSS, with custom fonts, colors, and layout to create a unique and engaging visual experience.

Loading State: When loading data or transitioning between screens, the website displays a loading animation to inform users that content is being loaded. This is implemented using CSS and JavaScript to create a smooth and seamless loading experience.


Timeline
Project execution will start in Week 4 of MU. Based on the previously defined requirements, user stories and technical challenges, use the following table to scope out and plan a timeline for deliverables over Week 4 - 9. You can be as detailed as you need, ranging from simply mentioning the user stories, or dividing them into sub-tasks.

You are free to modify the table, add / remove rows or columns, whatever fits your style! The important thing here is that you focus and prioritize certain aspects of your project so you don’t get behind and are ready to deliver the MVP - remember your required features should be code complete before the end of Week 8, including both technical challenges!

We also encourage you to leverage project tracking tools such as GitHub Issues or Meta’s internal Tasks / GSD tooling to keep manage individual units of work.

MU Week
Project Week
Focus
User Stories
4
1
Focus on the components that will serve as the skeleton of your project. You will probably be using most of what you learned in CodePath to set up things like the client and server repositories, initial routing, login / registration, creating a database with object models, etc.
User can login
User can create an account
User can see the the recipes displayed in the home page
Database will object models will be created
Basic CSS on HomePage
5
2
Week 5 and 6 should be where you focus on the specific requirements of your project.
User can click on a recipe and see the information (link to a new page)
User can like, save on a recipe
User can search and filter 
User can submit a form to get a page displaying recipes based on their ingredients available
6
3
By this point, you should be getting started with your technical challenges as well.
User can comment on recipes(real-time chatting without reloading the page)
User can make a grocery list and see it on their users page
Get started on machine learning for personalized recipes
7
4
You should focus on finishing your MVP and core requirements. By this point, you should be done with at least one of your technical challenges.


8
5
Continue work on finishing touches and stretch goals for your MVP. By this point, your core functionality and both TAPs should all be in place. It is also a good point to start working on stretch goals that could further expand on the functionality (and technical complexity) of your project.

This week you also have to submit your self-review, make sure you allocate enough time for this alongside your final submission for your project!


9
6
It’s time to show others what you have built! Work on a presentation and demo that you will present to other interns to showcase your work. You are also free to continue polishing and expanding on your project!


10
7
For this week, we have a bunch of extra activities prepared to give you a quick dive of what it is to work at Meta. You will find activities around using internal tools and frameworks, and even committing code to our internal repositories.





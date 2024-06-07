# Reading Log
#### Video Demo:  https://www.youtube.com/watch?v=lqOnY7F7p_c
#### Description: A way to keep track of all the books you've read recently.

**An Overview of The Project**
Reading Log is a web application that allows you to create an account and log all the books you've read recently. While logging your books you can include details like the book's title, author, your review of it, and a rating as well. Once you've logged in your information, the book's details will appear on the homescreen, along with a "remove" button if you wish to get rid of it as well.

For this project, I used HTML, CSS, Flask, Python, and SQL. Here's a look at all the files I used along with more information regarding them.

**Static**
***Styles.css***
In the "Static" folder I have created a file called Styles.css which describes the basic formatting I've used for most of the website
Firstly, I start with the Body and provide a gradient background, the font I use throughout the document is Arial.
Then for the ".card" class , which I use to diplay the books and their details on the homepage, styles a container element, giving it rounded corners and a subtle shadow effect to create a card-like appearance.
Buttons with the class ".btn-primary" have a background color of blue and when hovered over, the background color becomes a slightly darker shade.
Form input fields styled with the ".form-control" class have rounded corners and no box shadow by default. However, when clicked on, they gain a box shadow effect, indicated by a light blue glow.

**Templates**
***add_book.html***
This html page is used when the user wants to add another book to their reading log. It follows the same style as the base.html pageand has input functions for the author's name, the book's title, your review, and your rating.
***apology.html***
Apology.html generates an apology message if the user inputs any incorrect information or forgets to fill in a field while registering or logging in.
***base.html***
This page generated the basic HTML formatting that is used throughout the web page.
***book_detail.html***
This gives us the book details that we have already previously inputted and allows us to view it again through our homepage
***index.html***
This is the homepage of the site and it contains features such as a nav bar that show us the menu options and this page will also display all our books once we finish adding them.
***login.html***
This page allows us to log in and contains a form that lets us input details like our email address and password
***register.html***
Similar to login.html, however this also has an additional field that allows first time users to confirm their password.

**App.py**
App.py is the main code for the web application and I integrated flask to create the site.
First, I imported different libraries such as render_template, and redirect from Flash, SQL from the cs50 library, datetime and timezone from datetime, and also generate_password_hash from werkzeug.security. I also imported Book, Review, apology, User which I defined in models.py

Created and configured with a secret key for sessions and database URI for SQLite and ensured that all the tables were created in the database.

I've included various different routes such as - @app.route('/') which defines the index, that is the homepage; @app.route('/book/<int:book_id>') this shows specific details about a book; @app.route('/add', methods=['GET', 'POST']) this handles adding a new book and its review, and on POST request, it saves the book and review to the database and flashes a success message; @app.route('/delete/<int:book_id>', methods=['POST'])- this is for when you want to delete the book from the log; and also @app.route("/login", methods=["GET", "POST"]) for logging in and @app.route("/register", methods=["GET", "POST"]) for user registration.

In the route for adding books, @app.route('/add', methods=['GET', 'POST']) decorator defines the URL endpoint /add and specifies that this route accepts both GET and POST requests. The code extracts data from the form fields using add_book.html, including the book's title, author, review text, and rating. The new book object is added to the database session and committed, saving it to the database. The user is redirected to the home page using redirect and url_for. If the request is a GET request (i.e., the user is visiting the page to add a new book), the add_book.html template is rendered, displaying the form to the user.

In the route for registration, @app.route("/register", methods=["GET", "POST"]), decorator defines the URL endpoint /register and specifies that this route accepts both GET and POST requests. If the incoming request is a GET request, the registration form is rendered using the register.html template. The code extracts data from the form fields using request.form.get, including the email, password, and password confirmation. The program checks if the email is already in the database and also checks if the confirmation=password, then only does it allow you to register.

**Models.py**
Models.py defines the database models for a Flask application and includes utility functions for rendering apology messages and requiring login for certain routes.
It defines the 'user' and also includes the columns id, email, password. The book class represents books in the database, and has the columns id, title, author. The reviews class shows reviews in the database and has the columns id and text and book_id (which cannot be empty). We also define functions such as apology which generate an apology message when enough information is not provided.

**init_db.py**
this helps create tables in the databse. We import app and db from the app module along with user from models which was have already previously defined. with app.app_context()- sets up the application context. This is necessary because the database operations require access to the application context.db.create_all()- creates all the tables defined in the models if they don't already exist. This will create the tables for User, Book, Review, and any other models which are defined and imported.


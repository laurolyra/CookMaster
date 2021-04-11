# Project Name: Cookmaster

This project was entirely created as a prerequisite to measure my _NodeJS_ skills on Trybe's _Software Development_ course.

## What's been done here:

I've made an recipe managing sistem using _NodeJS_, built upon an MVC (Model-View-Controller) architecture. I'ts possible to **C**reate, **R**ead, **U**pdate and **D**elete as many recipes as you want from a database in SQL.

## Installing

1 - Clone this repo

`git clone git@github.com:laurolyra/CookMaster.git`

2 - Go to the project's directory

`cd CookMaster`

3 - Install all the dependencies

`npm install`

6 - Execute script `create_table.sql` to create the database.

5 - Start the application

`node index.js`

# Fulfilled Requirements

Every requirement down below reffers to business rules defined by Trybe, which I couldn't change to another pattern or use another technology.

Models, Views and Controllers were developed from a template containing the code for user login and logout, as well as a middleware used in all route that needed some authorization.

## Pages

### View Functionalities

## 1 - Main page

The page can be acessed through the main route (`/`).

For each recipe, it's shown only its name, its publisher's name, and a link guiding the user to read the how-to.

There is also an button written "Nova Receita" ("new recipe"), that is shown **only when there is a user logged in**.

## 2 - Recipes page

This screen is accessible through the endpoint `/recipes/:id` and shows a recipe's name, ingredients and preparation.

If the logged user's ID is the same from the one who created the recipe, two buttons will be shown: one named "Editar receita" ("edit recipe") and other named "Excluir receita" ("delete recipe"). These two buttons bring the user to the page "edit recipe" and "delete recipe", respectively.

These buttons won't appear if there isn't a logged user.

## 3 - User register

To register a user, it's necessary to fill every field on the register page - such as E-mail, Senha ("password"), Nome ("name") and Sobrenome("last name"). The ID is generated automatically.

All field validations are done in backend, and a message is sent to frontend through a property passed to EJS.

## 4 - Recipes creation page

This page can be accessed on the endpoint `/recipes/new`.

Recipes' name, ingredients, preparation and author fields are required. Like user registration's page, recipes' ID are generated  automatically.

## 5 - Recipes edition page

This page is accessible through the endpoint `/recipes/:id/edit` and its form is sent by POST to endpoint `POST /recipes/:id`.

When loaded, this page already shows all the information about the recipe.

Only the user who posted the recipe is allowed to edit it.

If the edition is successful, the user is redirected to the recipe page, which will show the updated information.

Every field is validated in backend.

## 6 - Recipes deletion page

This page is accessed through endpoint `/recipes/:id/delete`. It can only be accessed by a user who posted the recipe.

To confirm the deletion, user must type his/her password. This form is sent to the endpoint `POST /recipes/:id/delete`, and it will delete the recipe only if typed password is correct. If not, the user will be redirected to deletion page, now showing the message "Senha incorreta. Por favor, tente novamente" ("wrong password. Please, try again")

If typed password is correct, the user will be redirected to the main page.

## 7 - Recipes research page

The webpage is available through the endpoint `/recipes/search`.

A text input is displayed along with a "search" button. the inmput content is sent to the endpoint `GET /recipes/search` through the parameter `q` in the query string.

At the backend, the text input value is available through the "q" property of the `req.query` object. If no data is informed for the search, the view is rendered only with the search field. if a value is informed, a similar list to the recipe list screen is displayed, containing title, name of person who signed in and a link foir each recipe.

To perform the search, the recipe controller requests that the model search for recipes **containing in its name** the typed value in the search input.

## 8 - Creating the "My Recipes" page

The link to access this page is only available to logged users. 

The page is available though the endpoint `/me/recipes` and renderes a list equal to the list displayed at the Recipe List page, populated with the recipes registered by the logged user.

If the person who is not logged in accesses this page, they are redirected to the login page.

## 9 - Creating a page for Editing User

The link to access this page is only available to logged users.

Each user can only edit their own profile. For such, the backend extracts the ID from the selected user from the property `req.user` and not from the request body. This is the ID sent to the model to perform the user update.

This page is available through the endpoint `/me/edit`, and the form is sent to the endpoint `POST /me`.

If the unlogged user tries to access the page, they are redirected to the login page. (The middleware `authMiddleware` implements this functionality, so don't forget to use it here). 

The user ID cannot be edited. Neither at the screen, nor by Postman request.


## 10 - Using "includes" from EJS to render pages navbar

Part of the HTML will be duplicated in every page such as, for example, the navigation bar.

For such repeated content, `includes` from EJS was used.

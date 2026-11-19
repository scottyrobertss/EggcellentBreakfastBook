# Eggcellent Breakfast Book

A MySQL recipe database of 60+ breakfast dishes from around the world, with a Python command-line app for searching recipes and saving favorites. Built for a university Database course.

## Features

- **User accounts:** register and sign in
- **Recipe search:** by dish name, by ingredient, or by region (e.g., USA, France, Japan, Mexico)
- **Favorites:** save recipes to your account and view them later
- **Nutrition and dietary data:** calories, macros, and dietary flags (vegetarian, vegan, pescatarian, kosher, halal, allergens) for each dish

## Database Design

The database (`FoodDBRefined.sql`) has 6 related tables:

| Table | What it stores |
| --- | --- |
| `FoodItems` | Each dish's name, cook time, rating, region, and difficulty |
| `NutritionalValue` | Calories, carbs, fats, protein, and serving size per dish |
| `Diet` | Dietary flags and allergens per dish |
| `Recipe` | Ingredients, prep time, and step-by-step instructions |
| `User` | Registered app users |
| `Favorites` | Which recipes each user has saved |

`NutritionalValue` and `Diet` link to `FoodItems` by `FoodID`, and `Favorites` links `User` to `Recipe`. All three use foreign keys with `ON DELETE CASCADE`, so deleting a dish or user also removes its related rows.

## Tech Stack

- **Database:** MySQL
- **App:** Python 3 with `mysql-connector-python`

## How to Run

1. Install MySQL and Python 3, then install the connector:

   ```bash
   pip install mysql-connector-python
   ```

2. Create the database and load the sample data:

   ```bash
   mysql -u root -p < FoodDBRefined.sql
   ```

3. Set your MySQL password as an environment variable, then start the app:

   ```bash
   # macOS / Linux
   export DB_PASSWORD='your_mysql_password'
   python app.py

   # Windows PowerShell
   $env:DB_PASSWORD='your_mysql_password'
   python app.py
   ```

4. Register a new account, sign in, and search for recipes.

## Possible Improvements

- Hash user passwords (e.g., with `bcrypt`) instead of storing them as plain text
- Add search by dietary needs (e.g., vegan or allergen-free) using the `Diet` table
- Show nutrition info alongside search results

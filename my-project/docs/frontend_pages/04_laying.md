Now let’s focus on transforming our starter code into a Recommender app for our Amazon product data!

First, let’s remove the starter code that was provided when we created the tg_flutter application. Before deleting anything, skim over the comments provided in the file. These are helpful to understanding each piece of the Flutter puzzle. 

Let’s start with thinking about and laying down the foundation of our app’s structure. 

What do our TigerGraph Queries look like? What information are we getting from each of them? And how do we display this information to the user? 

We have ‘userExists’, ‘productExists’, ‘topProducts’, and ‘recommender’.

The user query and the recommender query have to do with User information and the input is a user name that exists in our data. So let’s keep those two on one page! Let’s put the product exists and top products queries on their own separate page.

So now we know we must create multiple pages with navigation. 

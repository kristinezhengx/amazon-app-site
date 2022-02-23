Let's begin by getting our Firebase storage ready!

Go to your project dashboard on Firebase Console, select “Storage” from the left-hand menu then you can see the bucket path as shown in the screenshot below:

![Firebase Registration](../assets/firebase/firebase3.png)

You don’t have to manually add the path to your Flutter code because it will be handled automatically by Firebase packages.

For simplicity’s sake, we will NOT implement authentication in this example. Therefore, we need to change the rules for Firebase Storage to be public, like this:

![Firebase Registration](../assets/firebase/firebase5.png)


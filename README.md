# Simple Android 2 

### So this is another Android Walkthrough that will show you how to use the [Android AsyncTask](http://developer.android.com/reference/android/os/AsyncTask.html) class to query for data in the background of your android activities as well as query the [Sugabus API](http://api.rutgers.edu/) and render that data into our activity. 

### You already know that most of the action is in [mainActivity.java](https://github.com/DavidAwad/SimpleAndroid2/blob/master/app/src/main/java/edu/rutgers/rumad/rumadworkshoptwo/completed/MainActivity.java) and [mainActivity.xml](https://github.com/DavidAwad/SimpleAndroid2/blob/master/app/src/main/res/layout/activity_main.xml), so let's take a quick look at those. 

Not much is happening in our xml, we define a button and a text box that currently only contains a placeholder. 
Let's talk on a high level about what the app will do at first. 

A user will press a button on their android phone, the app will then find that information from the Sugabus API, and we will then render some of that information unto the screen. yay!  

So why use `AsyncTask` in the first place? Here's the idea, our curent activity has control of the user. If we want to make queries for information, instead of forcing the user to wait, we could preemptively look up information without holding up the current user activity*. So what we say is let's run our query in a *separate thread*, and do other things with the processor and the user while our app has priority. This is important because you will need your apps to be snappy! 

*For a better understanding of why this should be done this way, check out the docs on the [Android Activity Lifecycle](http://developer.android.com/reference/android/app/Activity.html). 

# Resources
## [Android Activity Lifecycle](http://developer.android.com/reference/android/app/Activity.html)


# Contributors

## Obvious huge thank you to [Shreyas Hirday](https://github.com/shreyashirday) for the original codebase. 

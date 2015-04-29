# Simple Android 2 

### So this is another Android Walkthrough that will show you how to use the [Android AsyncTask](http://developer.android.com/reference/android/os/AsyncTask.html) class to query for data in the background of your android activities as well as query the [Sugabus API](http://api.rutgers.edu/) and render that data into our activity. 


#### You already know that most of the action is in [mainActivity.java](https://github.com/DavidAwad/SimpleAndroid2/blob/master/app/src/main/java/edu/rutgers/rumad/rumadworkshoptwo/completed/MainActivity.java) and [mainActivity.xml](https://github.com/DavidAwad/SimpleAndroid2/blob/master/app/src/main/res/layout/activity_main.xml), so let's take a quick look at those. 

Not much is happening in our xml, we define a button and a text box that currently only contains a placeholder. 
Let's talk on a high level about what the app will do at first. 

Looking inside of the java, that's where most of the action is. You know at a high level that we are going to talk to Sugabus somehow. This is typically done using an asynchronous task. Let's look at some code. 

```java
private  class getSugasBusData extends AsyncTask<Void,Void,Object>{
        //base url for all our endpoints
        String baseUrl = "http://runextbus.heroku.com/";
        //this method is executes the following code in the background thread
        //so that there is no crashing because of interaction with UI Thread
        @Override
        protected Object doInBackground(Void... params) {
            //initialize http client
            HttpClient client = new DefaultHttpClient();
            //can change this to make any url you want
            String endpoint = getActiveUrl();
            //initialize a GET request with whatever url you want, im using active as an example
            HttpGet get = new HttpGet(endpoint);
            try{
                //execute the get request and store response
                HttpResponse response = client.execute(get);

                //get status code of http request
                StatusLine statusLine = response.getStatusLine();

                //initialize byte outputstream to store data
                ByteArrayOutputStream bos = new ByteArrayOutputStream();

                //store data from http response
                response.getEntity().writeTo(bos);

                //close the stream
                bos.close();

                //if the status code is OK
                if(statusLine.getStatusCode() == HttpStatus.SC_OK){

                    //return data in a string
                    return bos.toString();

                }else{

                    //something got messed up
                    return  null;
                }
            }catch (IOException e){
                //lets see what the error was
                Log.e("ERROR",e.getMessage());
                return  null;
            }
        }
    }
```

So why use `AsyncTask` in the first place? Here's the idea, our curent activity has control of the user. If we want to make queries for information, instead of forcing the user to wait, we could preemptively look up information without holding up the current user activity*. So what we say is let's run our query in a *separate thread*, and do other things with the processor and the user while our app has priority. This is important because you will need your apps to be snappy! 

*For a better understanding of why this should be done this way, check out the docs on the [Android Activity Lifecycle](http://developer.android.com/reference/android/app/Activity.html). 

# Resources
## [Android Activity Lifecycle](http://developer.android.com/reference/android/app/Activity.html)


# Contributors

## Obvious huge thank you to [Shreyas Hirday](https://github.com/shreyashirday) for the original codebase. 

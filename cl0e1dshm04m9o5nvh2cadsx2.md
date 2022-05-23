## How to filter an ArrayList in android using Java

So we all have seen that in android if we want to pass Data from one activity to another we generally do with the Intents and sometimes with bundle.

But sometimes we are in a need of large data filtering from one activity to another, let me clear it. Suppose if you want to filter an arrayList by using just another single activity apart from MainActivity then we are in a big difficulty.

So there is a away that we can do that with intents, but why do we make our code complex to understand if the same thing we can do it with Bundle class.

let me Clear it for you

Whenever we use ```intent.putExtra()``` to map the bundle with a name at runtime our application somtimes crashes while filtering the arraylist to another activity

so for that intent.putExtras() is used

>  To Filter the arraylist ``` intent.putExtras() ``` is the best Practice 

Here is the Code to filter an arrayList in mainActivity.Java
```
// The ArrayList
ArrayList<String> arrayList2 = new ArrayList<>();
arrayList2.add("heading 1");
arrayList2.add("heading 2");

// Now we'll Put the data in a bundle

 Intent intent=new Intent(getApplicationContext(), Activity_2.class); // specifying the second activity
 Bundle bundle=new Bundle();

 for(int  i=0;i<arrayList2.size();i++)
  {
   bundle.putString("arrayList", arrayList2.get(i));
  }

intent.putExtras(bundle);
startActivity(intent);
``` 

Now in another activity we can get this arrayList using the same bundle Activity2.Java
```
Intent intent=intent.getIntent();
Bundle bundle=intent.getExtras();

// here we can filter our arraylist

if(bundle.getString("arrayList").equals("heading 2")){
  // Your Code Here For Filtering
}

// Thats it

```
So by doing this way we can filter any type of arrayList in android and we can reduce the use of lots and lots of activities.

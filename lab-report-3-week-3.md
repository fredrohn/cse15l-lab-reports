# Lab Report Week 3

In week 2, we learned about building our own servers and running them locally and remotely. 

In week 3, we learned about debugging

## Part 1

This is the code from my search engine: 
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> items = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return items.toString();
        } else if (url.getPath().equals("/search")) {
            ArrayList<String> temp = new ArrayList<>();
            System.out.println("Path: " + url.getPath()); //accessory
                String[] parameters = url.getQuery().split("="); 
                if (parameters[0].equals("s")) {
                    for(int i=0; i < items.size(); i++){
                        if(items.get(i).contains(parameters[1])){
                            temp.add(items.get(i));
                        }
                    }
                    return temp.toString();
                }
            return "404 Not Found!";
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("="); 
                if (parameters[0].equals("s")) {
                    items.add(parameters[1]);
                    return parameters[1] + " added!";
                }
            }
            return "404 Not Found!";
        }
    }
}

class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}


```

Build and run the server by using these commands:
```
$ javac SearchEngine.java
$ java SearchEngine 4000
```
Now that the server is running at port 4000, you can access it using the link in the console. In this case, the console showed this: 
```
Server Started! Visit http://localhost:4000 to visit.
```

This is what it initially looked like: 
![initial-state-screenshot](week-3-photos/initial-state-screenshot.png)

I added three items to the array by typing different URLs. Here is that that all looked like: 

![added-1-screenshot](week-3-photos/added-1-screenshot.png)

![added-2-screenshot](week-3-photos/added-2-screenshot.png)

![added-3-screenshot](week-3-photos/added-3-screenshot.png)

This is what the final state of the array looked like: 

![final-state-screenshot](week-3-photos/final-state-screenshot.png)

I queried the array for strings that contained "ap". This is what that printed: 

![query-screenshot](week-3-photos/query-screenshot.png)

Everytime I clicked enter after I typed a new url path, the handleRequest() method was called. 

In the first screenshot, the handlerequest method was called and the URL path was only "/", so the code within the first if condition was triggered. This caused it to print out the contents of the items Array List. There are no values, which is why you see square brackets with no contents. 

In the following screenshots where I included add into the URL, the third if condition (else) was triggered. It checked whether or not the string contained "add", and looked for the item to add. In the first of those three screenshots, that word would be "apple". It then adds that String to the items Array List. It then prints the string "apple added!" to let the user know that the processing is complete. 

To see what values were stored, I deleted the entire path except for the "/". This triggered the first if condition and printed the contents of items. Now that those three items have been added, they are visible in the window. 

Finally, when you type search into the path, it triggers the second if condition (else if). It takes the part of the query that has the string I want to search for, and checks which elements of the items ArrayList contains that string, and stores it in a temporary Array List. In this case, that would be "ap". That gets returned as a string gets printed. This is visible in the window. 

## Part 2

### Debugging the reverseInPlace() method

This is the code for the reverse in place method:

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

I tried two failure inducing inputs to make sure that I understood what was wrong with the array:

```
input1 = {1,2,3}
input2 = {1,2,3,4,5,6}
```
To give some idea of what happened, this is the symptom produced and message displayed when I test input2 through JUnit: 
```
There was 1 failure:
1) testReverseInPlaceAgain(ArrayTests)
arrays first differed at element [3]; expected:<3> but was:<4>
```
What happened was, the method turned {1,2,3,4,5,6} into {6,5,4,4,5,6}. The reason for this symptom is a relatively straighforward bug: 

It begins at the 0 index and replaces the value with the last index, without actually saving the first index anywhere. Then it moves on to the second index and second last. This means, as it works its way through the array, the values from the lower half of the array all disappear. That is why only half the array is changed. 

Instead of simply throwing out the original values, the method should store them in a temporary array called reversedArray before filling it back in. This is my fix:

```
static void reverseInPlaceFixed(int[] arr) {
    int[] reversedArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      reversedArray[i] = arr[arr.length - 1 - i];
    }
    for (int i = 0; i < arr.length; i++) {
      arr[i] = reversedArray[i];
    }
  }
```

###Debugging the filter() method

This is the code for the filter() method: 

```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
  ```

  The failure inducing input I used is this:

  I am showing the whole Test because it is easier than describing the Array List
  ```
  public class ListTests {
    @Test
    public void testListExamples(){

        List<String> input = new ArrayList<>();
        input.add("Fred");
        input.add("Frederick");
        input.add("Rohn");
        input.add("fortress");

        List<String> toCheck = new ArrayList<>();
        toCheck.add("Frederick");
        toCheck.add("fortress");
        
        assertEquals(toCheck, ListExamples.filter(input, new longString()));
    }
}
  ```

  This is the symptom/error message displayed if you test this using JUnit: 

  ```
  1) testListExamples(ListTests)
java.lang.AssertionError: expected:<[Frederick, fortress]> but was:<[fortress, Frederick]>
```

The bug is in the way the code adds the element to the Array List. It should be adding the element at the end, but instead it adds it to the beginning. That is why the output is backwards.

Instead of `using add(0, s);`, leave out the index. 

This is my fix: 

```
static List<String> filterFixed(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }
  ```




# My javascript toolBox

## This Book:
 Coding is all fun and rosy till you hit a concept you would want to code but you cant code it! you know why? because you lack the initiative, exposure or experince to know the right comination and placement of functions and utilities needed to acheive that concept. Today I  decided to document toolz I learned the hard way. Most of this code snippet were gotten after tons of research and going back and front till I was able to stumble on the necessary requirement (initiative, exposure and exeperince) mind power to code it.

##  Load Dynamic Object:
>I am a fan of javascript object template literals. When I want to code a dynamic page with just plain javascript and html css, I first create the static page and store the text markup in a javascript variable (object variable). With the content saved in an object I can then easily load them when a button or expected action is triggered. Now lets have an example for better example, look below

```
    var template = {
          firstSlide: `<header> Welcome to dannyokec group </header>
                          <body>
                              <article> ... </article>
                              <side> .... </side>
                            </body>
                         `,
           secondSlide: `<header> Our businesses </header> 
                           <body>
                              <article> ....
                              ........
                           `
             thirdSlide: `...`
    }
    
    var whatToLoad = "secondSlide"; // This is where we store what property to load from the object, usually this property to load is generated dynamically from a button clicked, a network response or from a user selection.
    
    // I love using jquery so i will be using most part of jquery on this example
    
    $('viewer').html(template[whatToLoad]) // this line loads a html content from what ever is passed into it. On this line, we are loading the html from the  object called template. You would also notice we are using the variable whatToLoad as a property(key). This would run easily because the object is one layer and not nested deep, the moment we introduce a deeper layer our code runs into execution issues.
    
   # Example with a nested object
   
       let template = {
          firstSlide: { "body":`<header> Welcome to dannyokec group </header>
                          <body>
                              <article> ... </article>
                              <side> .... </side>
                            </body>
                         `,
                         "footer":`<footer> Contact us ... </footer>`
                         }
    }
    
        let whatToLoad = "firstSlide.footer";

    
    $('viewer').html(template[whatToLoad])  // This will result an error, the error is as a result of javascript been unable to nest inwardly by default
    
    # The solution is to create a function that would automatically load dynamic object. i will call objDyn
    
              function objDyn(obj,path) {
              var schema = obj;  // a moving reference to internal objects within obj
              var pList = path.split('.');
              var len = pList.length;
              for(var i = 0; i < len-1; i++) {
                  var elem = pList[i];
                  if( !schema[elem] ) schema[elem] = {}
                  schema = schema[elem];
              }

             return schema[pList[len-1]] 
          }
          
          
           
       let template = {
          firstSlide: { "body":`<header> Welcome to dannyokec group </header>
                          <body>
                              <article> ... </article>
                              <side> .... </side>
                            </body>
                         `,
                         "footer":`<footer> Contact us ... </footer>`
                         }
    }
    
        let whatToLoad = "firstSlide.footer";

    
    $('viewer').html(objDyn(template,whatToLoad))  // Now the what to load would be used to inwardly to match the property that fits it
    


```


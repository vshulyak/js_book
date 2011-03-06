Deffered
============
http://thomasdavis.github.com/tutorial/jquery-create-your-own-deferred.html

jQuery 1.5 - create your own deferred object with parameters

jQuery has just recently released version 1.5 which now contains $.when and $.then, yay! There are many tutorials already on how to use these new functions. All the examples used $.ajax calls which are setup by jQuery to be used as deferred objects so I found it difficult to implement my own deferred objects. I found this guide which is great and covers most of what you need to know.

The tutorial covers how to create your own deferred objects but doesn't include passing parameters to $.then call backs. So after playing around a little bit and reading the jQuery source I figured it out and have included it below.

I have seen some people asking on how to do this so hopefully it helps! As usual post any mistakes I made =D


function myFunc(){
    return $.Deferred(function( deferred_obj ){
        $("body").css("background", "#ff0000"); // Example
        deferred_obj.resolve( "these", "are", "my", "parameters" );
        // Call resolve when you are ready to continue, in animation callbacks etc
    }).promise();
}
  
$.when( myFunc() )
    .then(function(p1, p2, p3, p4){
        console.log( p1 + p2 + p3 + p4);
});

So it's pretty easy and you should start using them immediatly!





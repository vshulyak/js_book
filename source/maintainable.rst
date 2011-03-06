How to Write Maintainable OO JavaScript Code
================================================

http://msdn.microsoft.com/en-US/scriptjunkie/gg602402.aspx

Writing maintainable Object-Oriented (OO) JavaScript will save you money and make you popular. Don't believe me? Odds are that either you or someone else will come back and work with your code. Making that as painless an experience as possible will save time, which we all know equates to money. It will also win you the favor of those for whom you just saved a headache. But before we dive into writing maintainable OO JavaScript, let's just take a quick look at what OO is all about. If you know already about OO, feel free to skip the next section.

What is OO?
-------------------

Object-oriented programming basically represents physical, real-world objects that you want to work with in code. In order to create objects, you need to first define them by writing what's called a class. Classes can represent pretty much anything: accounts, employees, navigation menus, vehicles, plants, advertisements, drinks, etc... Then, every time you want to create an object to work with, you instantiate one from a class. In other words, you create an instance of a class which gives you an object to work with. In fact, the best time to be using objects is when you'll be dealing with more than one of anything. Otherwise, a simple functional program will likely do just as well. Objects are essentially containers for data. So in the case of an employee object, you might store their employee number, name, start date, title, salary, seniority, etc... Objects also include functions (called methods) to handle that data. Methods are used as intermediaries to ensure data integrity. They're also used to transform data before storing it. For example, a method could receive a date in an arbitrary format then convert it to a standardized format before storing it. Finally, classes can also inherit from other classes. Inheritance allows you to reuse code across different types of classes. For example, both bank account and video store account classes could inherit from a base account class which would provide fields for profile information, account creation date, branch information, etc... Then, each would define its own transactions or rentals handling data structures and methods.

Warning: JavaScript OO is different
In the previous section I outlined the basics of classical object-oriented programming. I say classical because JavaScript doesn't quite follow those rules. Instead, JavaScript classes are actually written as functions and inheritance is prototypal. Prototypal inheritance basically means that rather than classes inheriting from classes, they inherit from objects using the prototype property.

Object Instantiation
-------------------

Here's an example of object instantiation in JavaScript:

// Define the Employee class
function Employee(num, fname, lname) {
    this.getFullName = function () {
        return fname + " " + lname;
    }
};
 
// Instantiate an Employee object
var john = new Employee("4815162342", "John", "Doe");
alert("The employee's full name is " + john.getFullName());
There are three important things to note here:

I uppercased the first letter of my "class" function. That important distinction lets people know that it's for instantiation and not to be called as a normal function.
I use the new operator when instantiating. Leaving it out would simply call the function and result in problems.
Though getFullName is publicly available because it's assigned to the this operator, fname and lname are not. The closure created by the Employee function gives getFullName access to fname and lname while allowing them to remain private from everyone else.
Prototypal Inheritance
Now, here's an example of prototypal inheritance in JavaScript:

// Define Human class
function Human() {
    this.setName = function (fname, lname) {
        this.fname = fname;
        this.lname = lname;
    }
    this.getFullName = function () {
        return this.fname + " " + this.lname;
    }
}
 
// Define the Employee class
function Employee(num) {
    this.getNum = function () {
        return num;
    }
};
// Let Employee inherit from Human
Employee.prototype = new Human();
 
// Instantiate an Employee object
var john = new Employee("4815162342");
    john.setName("John", "Doe");
alert(john.getFullName() + "'s employee number is " + john.getNum());
This time, I've created a Human class which contains properties common to humans--I moved fname and lname there since all humans, not just employees have names. I then extended the Employee class by assigning a Human object to its prototype property.

Code Reuse Through Inheritance
-------------------

In the previous example, I split the original Employee class in two. I moved out all the properties common to all humans into a Human class, and then caused Employee to inherit from Human. That way, the properties laid out in Human could be used by other objects such as Student, Client, Citizen, Visitor, etc... As you may have noticed by now, this is a great way to compartmentalize and reuse code. Rather than recreating all of those properties for every single type of object where we're dealing with a human being, we can just use what's already available by inheriting from Human. What's more, if we ever wanted to add a property like say, middle name, we'd do it once and it would immediately be available to everyone inheriting from Human. Conversely, if we only wanted to add a middle name property to just one object, we could do it directly in that object instead of adding it to Human.

Public and Private
-------------------

I'd like to touch on the subject of public and private variables in classes. Depending on what you're doing with the data in an object, you'll want to either make it private or public. A private property doesn't necessarily mean that people won't have access to it. You may just want them to go through one of your methods first.

Read-only
-------------------

Sometimes, you only want a value defined once at the moment the object is created. Once created, you don't want anyone changing that value. In order to do this, you create a private variable and have its value set on instantiation.

function Animal(type) {
    var data = [];
    data['type'] = type;
    this.getType = function () {
        return data['type'];
    }
}
 
var fluffy = new Animal('dog');
fluffy.getType(); // returns 'dog'
In this example, I create a local array called data within the Animal class. When an Animal object is instantiated, a value for type is passed and set in the data array. This value can't be overwritten as it's private (the Animal function defines its scope). The only way to read the type value once an object is instantiated is to call the getType method that I've explicitly exposed. Since getType is defined inside Animal, it has access to data by virtue of the closure created by Animal. This way, people can read the object's type but not change it.

It's important to note that the "read-only" technique will not work when an object is inherited from. Every object instantiated after the inheritance is performed will share those read-only variables and overwrite each other's values. The simplest solution is to convert the read-only variables in the class to public ones. If however, you must keep them private, you can employ the technique pointed out by Philippe in the comments.

Public
There are times however, that you'll want to be able to read and write a property's value at will. To do that, you need to expose the property using the this operator.

function Animal() {
    this.mood = '';
}
 
var fluffy = new Animal();
fluffy.mood = 'happy';
fluffy.mood; // returns 'happy'
This time our Animal class exposes a property named mood which can be written to and read at will. You can equally assign a function to public properties like the getType function in the previous example. Just be careful not to assign a value to a property like getType or you'll destroy it with your value.

Completely Private
Finally, you might find yourself in scenarios where you need a local variable that's completely private. In this case, you can use the same pattern as the first example and just not create a public method for people to access it.

function Animal() {
    var secret = "You'll never know!"
}
 
var fluffy = new Animal();

Writing a Flexible API
-------------------

Now that we've covered class creation, we need to future proof them in order to keep up with product requirement changes. If you've done any project work, or maintained a product long-term, you know that requirements change. It's a fact of life. To think otherwise is to doom your code to obsolescence before it's even written. You may suddenly have to animate your tab content, or have it fetch data via an Ajax call. Though it's impossible to truly predict the future, it is possible to write code that's flexible enough to be reasonably future proof.

Saner Parameter Lists
-------------------

One place where future-proofing can be done is when designing parameter lists. They're the main point of contact for people implementing your code and can be problematic if not well designed. What you want to avoid are parameter lists like this:

function Person(employeeId, fname, lname, tel, fax, email, email2, dob) {
};
This class is very fragile. If you want to add a middle name parameter once you've released the code, you're going to have to do it at the very end of the list since order matters. That makes it awkward to work with. It also makes it difficult to work with if you don't have values for each parameter. For example:

var ara = new Person(1234, "Ara", "Pehlivanian", "514-555-1234", null, null, null, "1976-05-17");
A cleaner, more flexible way of approaching parameter lists is to use this pattern:

function Person(employeeId, data) {
};
The first parameter is there because it's required. The rest is lumped together in an object which can be very flexible to work with.

var ara = new Person(1234, {
    fname: "Ara",
    lname: "Pehlivanian",
    tel: "514-555-1234",
    dob: "1976-05-17"
});
The beauty of this pattern is that it's both easy to read and highly flexible. Note how fax, email and email2 were completely left out. Also, since objects aren't order specific, adding a middle name parameter is as easy as throwing it in wherever it's convenient:

var ara = new Person(1234, {
    fname: "Ara",
    mname: "Chris",
    lname: "Pehlivanian",
    tel: "514-555-1234",
    dob: "1976-05-17"
});
The code inside the class doesn't care because the values get accessed by index like so:

function Person(employeeId, data) {
this.fname = data['fname'];
};
If data['fname'] returns a value, it gets set. Otherwise, it doesn't, and nothing breaks.

Make It Pluggable
-------------------

As time goes on, product requirements might demand additional behavior from your classes. Yet often times that behavior has absolutely nothing to do with your class's core functionality. It's also likely that it's a requirement for only one implementation of the class, like fading in the contents of one tab's panel while fetching external data for another. You may be tempted to put those abilities inside your class, but they don't belong there. A tab strip's responsibility is to manage tabs. Animation and data fetching are two completely separate things and should be kept outside the tab strip's code. The only way to future proof your tab strip and keep all that extra functionality external, is to allow people to plug behaviors into your code. In other words, allow people to hook into key moments in your code by creating events like onTabChange, afterTabChange, onShowPanel, afterShowPanel and so on. That way, they can easily hook into your onShowPanel event, write a handler that fades in the contents of that panel and everyone is happy. JavaScript libraries allow you to do this easily enough, but it's not too hard to work it out on your own. Here's a simple example using YUI 3.

<script type="text/javascript" src="http://yui.yahooapis.com/combo?3.2.0/build/yui/yui-min.js"></script>
<script type="text/javascript">
    YUI().use('event', function (Y) {
 
        function TabStrip() {
            this.showPanel = function () {
                this.fire('onShowPanel');
 
                // Code to show the panel
 
                this.fire('afterShowPanel');
            };
        };
 
        // Give TabStrip the ability to fire custom events
        Y.augment(TabStrip, Y.EventTarget);
 
        var ts = new TabStrip();
 
        // Set up custom event handlers for this instance of TabStrip
        ts.on('onShowPanel', function () {
            //Do something before showing panel
        });
        ts.on('onShowPanel', function () {
            //Do something else before showing panel
        });
        ts.on('afterShowPanel', function () {
            //Do something after showing panel
        });
 
        ts.showPanel();
    });
</script>
This example has a simple TabStrip class with a showPanel method. The method fires two events, onShowPanel and afterShowPanel. It's given the ability to do so by augmenting the class with Y.EventTarget. Once that's done, we instantiate a TabStrip object and assign a bunch of event handlers to it. This is our custom code for handling this instance's unique behavior without messing with the actual class.

Summary
-------------------

If you plan on reusing code either on the same page, website or across multiple projects, consider packaging and organizing it in classes. Object-oriented JavaScript lends itself naturally to better code organization and reuse. What's more, with a little forethought, you can make sure that your code is flexible enough to stay in use long after you've written it. Writing reusable, future-proof JavaScript will save you, your team and your company time and money. That's sure to make you popular.

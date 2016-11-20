# Tutorial 4 : jQuery Vaizr primer

If you want to go to the [previous tutorial](../tutorial/javascript) click [here](../tutorial/javascript)

If you want to go to the [next tutorial](../tutorial/add_and_edit) click [here](../tutorial/add_and_edit)

You can [download the tutorial resources here](../../downloads/tutorialresources.zip)

# Introduction

Understanding jQuery begins with an understanding of JavaScript. Sometimes jQuery is treated as an independent language that can be used instead of JavaScript. Although jQuery contains many features associated with programming languages, it is best thought of as a library that enhances JavaScript in specific situations. For this reason, JavaScript has been introduced before jQuery.

Before understanding jQuery however, it is worth taking a brief look at the Document Object Model (DOM), since jQuery is primarily a library for dealing with the DOM in a browser independent manner.

# Selection

The first thing we are going to do with Vaizr is select items from the screen.

Selecting elements obviously has no intrinsic value in its own right; we are eventually going to do something with these elements. A Vaizr selection will return zero or more Objects from the screen which contains details on the requested field name.

In order to perform a selection of an object, simply call the following function with the current screen items and the name of the field used in the screen:

     > For a field : 
     $.alfa.DlgBlocks.getFieldFromPage(pageItems, 'due_date')
     
     > For a button :
     $.alfa.DlgBlocks.getButton(pageItems, 'search')
     
     > For a table :
     $.alfa.DlgBlocks.getTable(pageItems, 'search_result_table')

The *pageItems* is a list of objects displayed in the screen. The are usually available with all the pre/post hooks provided in the screen. The second arguement ('due_date' in the above example) is the name of the item referred to in the screen.

The above line will provide an object with the following properties:

<ul>
<li>text field (date, checkbox , large-string)</li>
	<ul>
    <li>Id</li>
    <li>type</li>
    <li>value</li>
    </ul>
<li>Lov field</li> 
	<ul>
    <li>Id</li>
    <li>type</li>
    <li>value</li>
    <li>valuefield</li>
    <li>use_cache</li>
    <li>title</li>
    <li>size</li>
    <li>label</li>
    <li>displayfields</li>
    <li>editfields</li>
    <li>service</li>
    	<ul>
    	<li>dwr</li>
    	<li>parameters</li>
    		<ul><li>lov</li></ul>
    	</ul>
    </ul>
<li>Button</li>
	<ul>
    <li>Id</li>
    <li>action</li>
    <li>icon</li>
    </ul>
<li>Table</li>
	<ul>
    <li>type</li>
    <li>name</li>
    <li>id</li>
    <li>data</li>
    	<ul>
    	<li>columns</li>
    	<li>count</li>
    	<li>customColumns</li>
    	<li>displayLength</li>
    	<li>fnPaging</li>
    	<li>oncontextmenu</li>
    	<li>ondblclick</li>
    	<li>onkeys</li>
    	<li>paginationType</li>
    	<li>rows</li>
    	<li>selectMode</li>
    	<li>sortMode</li>
    	<li>tableHeight</li>
    	<li>totalCount</li>
    	<li>totalWidth</li>
    	</ul>
    </ul>
</ul>



# Events

The next aspect of jQuery to understand is events. When writing web applications, the application will need to respond to events initiated by the user.

These events may be any of the following:

* Clicking a link or button.
* Double clicking a button or link.
* Changing the value in a text field.
* Pressing a particular key inside an input field.
* Selecting an option in a select list.
* Focusing on an input field.
* Hovering the mouse over an element.

In addition to these user-initiated events, the application may wish to respond to browser-initiated events such as:

* The document has finished loading.
* The web browser window is resized.
* An error occurring.

This section will first explain the ways event listeners can be registered, and will then look at some of these events in detail.

Before beginning, we will add the examples above permanently to the tasks.html page. In order to do this, add the following block immediately before the closing </html> tag:

    <script>
       $('[required="required"]').prev('label').append( '<span>*</span>').children( 'span').addClass('required');
       $('tbody tr:even').addClass('even');
    </script>

This is a block of inline JavaScript. We will eventually provide more structure to the web application, and remove code such as this from the HTML page, but for now this is a simple way of including JavaScript code in the web page.

We will now begin by adding a simple event to the sample web application we have been working on. We will start by defining the task creation section of the screen (inside the first section element), to be hidden when we first come into the screen.

We will also provide it an id so we can easily refer to it:

    <section id="taskCreation" class="not">

The not class is defined in tasks.css, and provides a simple mechanism for hiding an element. It is defined as follows:
    .not {
        display:none;
    }

Next, we will modify the link with the text “Add Task” to have an id. This will allow us to select it more conveniently with jQuery:

    <a href="#" id="btnAddTask">Add task</a>

Finally, we will add the following code to the script section of tasks.html:

    $('#btnAddTask').click(function(evt) {
        evt.preventDefault();
        $('#taskCreation').removeClass('not');
    });

This code will be explained in detail below.

The entire page should now look like this (changes are encapsulated with two little comment blocks

    <!--starting new -->
       .. new block
    <!--endin new -->

The whole code block tasks2.html looks like

    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="utf-8">
    <title>Task list</title>
    <link rel="stylesheet" type="text/css" href="styles/tasks.css"
        media="screen" />
    <!--starting new -->
    <script src="scripts/jquery-1.11.1.js"></script>
    <!--ending new -->
    </head>
    <body>
        <header>
            <span>Task list</span>
        </header>
        <main>
    <!--starting new -->
            <section id="taskCreation" class="not">
    <!--ending new -->
                <form>
                    <div>
                        <label>Task</label> <input type="text" required="required"
                            name="task" class="large" placeholder="Breakfast at Tiffanys" />
                    </div>
                    <div>
                        <label>Required by</label> <input type="date" required="required"
                            name="requiredBy" />
                    </div>
                    <div>
                        <label>Category</label> <select name="category">
                            <option value="Personal">Personal</option>
                            <option value="Work">Work</option>
                        </select>
                    </div>
                    <nav>
                        <a href="#">Save task</a> <a href="#">Clear task</a>
                    </nav>
                </form>
            </section>
            <section>
                <table id="tblTasks">
                    <colgroup>
                        <col width="50%">
                        <col width="25%">
                        <col width="25%">
                    </colgroup>
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Due</th>
                            <th>Category</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Return library books</td>
                            <td><time datetime="2013-10-14">2013-10-14</time></td>
                            <td>Personal</td>
                        </tr>
                        <tr>
                            <td>Perform project demo to stakeholders</td>
                            <td><time datetime="2013-10-14">2013-10-14</time></td>
                            <td>Work</td>
                        </tr>
                        <tr>
                            <td>Meet friends for dinner</td>
                            <td><time datetime="2013-10-14">2013-10-14</time></td>
                            <td>Personal</td>
                        </tr>
                    </tbody>
                </table>
                <nav>
    <!-- starting new -->
                    <a href="#" id="btnAddTask">Add task</a>
    <!-- ending new -->
                </nav>
            </section>
        </main>
        <footer>You have 3 tasks</footer>
    </body>
    <!-- starting new -->
    <script>
        $('[required="required"]').prev('label').append( '<span>*</span>').children( 'span').addClass('required');
        $('tbody tr:even').addClass('even');
        $('#btnAddTask').click(function(evt) {
             evt.preventDefault();
            $('#taskCreation').removeClass('not');
        });
    </script>
    <!-- ending new -->
    </html>

If you reload the page, you should see that the task creation section (with all the input fields) is not displayed when the page initially loads. If you click the “Add task” button however, this section will immediately appear.

If you look at the event handler code you will see some familiar features. First, we select the element we wish to add an event listener to using standard jQuery selection criteria:

    > $('#btnAddTask')

Next we call the appropriate jQuery function on this element to add a click listener; this function is called __click__ and it accepts a JavaScript function as its parameter. In this example, the JavaScript function passed to the click function is created on the fly as an anonymous function. This could also have been written as follows:

    function btnAddClicked(evt) {
        $(evt.target).preventDefault();
        $('#taskCreation').removeClass('not');
    }

    $('#btnAddTask').click(btnAddClicked);

The technical term for the function we have passed to the click function is a callback. This is because the function is not executed immediately; it is executed when a specific event occurs (the user clicks the button). jQuery, like many other JavaScript libraries, makes extensive uses of callbacks, and we will see many other examples in the sections below.

You will also see that our function accepts a parameter called evt. When jQuery invokes the function we passed to it, it will provide an object as a parameter representing the event that has occurred.

The most useful feature that can be obtained from the event object is the element that caused the event. The same event listener may be added to many elements, therefore we will often need to find out which of these elements had the event invoked on it. This can be extracted from the event object as follows:

    evt.target

It may not be immediately obvious, but the object returned as the target is a plain DOM object rather than a jQuery wrapped DOM object. This may sound like a minor point, but it means that it is not possible to invoke jQuery functions on this element. For instance, if we attempt to call the __html__ function on this element, the following error will occur:

`tasks2.html:88 Uncaught TypeError: evt.target.html is not a function`

Whenever you are presented with a native DOM object, it is easy to convert it to jQuery wrapped object by selecting it:

    $(evt.target)

The result of this will expose all the standard jQuery functionality:

`Add task tasks2.html:88`

You will also notice the following line in the click handler:

    evt.preventDefault();

A single element can have multiple event listeners attached to it. Some of these will be added explicitly by the application, but the browser may add its own action implicitly. These implicit event listeners are called the default action of the element; for instance, a hyperlink has a default action that invokes its specified URL when it is clicked.

In this web application we do not want hyperlinks to exhibit this default behaviour, otherwise the page would be refreshed every time the user clicked a button. Therefore we call preventDefault on the event to signal that the element’s default action should be supressed.

   |   |   |
   |---|---|
   |   |Using hyperlinks instead of button elements is a personal preference. Many designers have historically preferred them, since they tend to be easier to style, and more flexible to use. There is however a strong argument in favour of using the button elements in these cases.|
   |   |   |

The final aspect of this event handler is the removal of the class that was causing this element to be hidden, which should be familiar code by now:

    $('#taskCreation').removeClass('not');

It is possible to add click listeners to any HTML element. For instance, we can add a feature to the __table__ so that when the user clicks a row it will highlight in bold. If they then click the row again it will return to normal.

The tasks.css file already contains a class that can set the text of an element to bold:

    .rowHighlight {
        font-weight:bold;
    }

As a first attempt at this code, we will try adding the following to the script block of tasks.html:


    $('tbody tr').click(function(evt) {
        $(evt.target).toggleClass('rowHighlight');
    });

This is adding a click listener to all rows in the __table__ body. When invoked, this will add the __rowHighlighted__ class to the element that was clicked.

If you debug this you will notice that the value of __evt.target__ is in fact the element that has been clicked on (the __td__ element) rather than the __tr__ element, therefore only a single cell highlights in bold.

   |   |   |
   |---|---|
   |   |The next chapter will address debugging JavaScript code. If you are unfamiliar with the Chrome debugger, and would like to see this for yourself, you may want to jump ahead to that chapter.|
   |   |   |

As a second attempt, we could try to find the __tr__ element that is the parent of the element that was clicked, and add the class to this element. This also will not work, since __td__ elements have been defined with normal font-styles in tasks.css, therefore they will not inherit font-style from their parents.

What we want to do is add this class to all the __td__ elements in the row that is selected. We could attempt this as follows:

    $('tbody tr').click(function(evt) {
        $(evt.target).siblings( ).toggleClass( 'rowHighlight');
    });

There are two problems remaining with this. The __siblings__ function returns a set of all the siblings, but leaves out the element that has been clicked, so all cells except the one clicked will highlight, we can solve this with the following:

    $('tbody tr').click(function(evt) {
        $(evt.target).siblings() .andSelf( ).toggleClass( 'rowHighlight');
    });

The next problem is the __td__ element that contains the __time__ element. If the __time__ element is clicked, the list of siblings will be empty, since the time element does not have any siblings. Before finding the siblings we therefore need to first find the closest __td__ element to the one clicked.

As mentioned earlier, the __closest__ function begins by examining the selected element, and only ascends the tree if that does not match the requirements. Therefore, the closest __td__ to a __td__ is itself, but the closest __td__ to a __time__ element is its parent.

The following code therefore meets our requirements:

    $('tbody tr').click(function(evt) {
        $(evt.target).closest( 'td').siblings( ).andSelf( ).toggleClass( 'rowHighlight');
    });

Finally, note that we are using the __toggleClass__ function. Rather than checking whether the elements have the class __rowHighlight__, and adding it if they don’t, and removing it if they do, we can let jQuery do the work for us.

In the examples above we are adding event listeners to elements in the document when the page is loaded. A complication with event listeners is that we might want to add them to elements that are not in the document yet. Due to the fact we can dynamically add elements to the DOM, we may want event listeners automatically added to these elements when they meet specified selection criteria.

If we consider the case of the event listener that highlights selected rows in the table, we may want this to work even if rows are dynamically added to the table after the page has loaded.

Fortunately jQuery has an elegant solution to this problem using the __on__ function. The first part of the solution involves specifying the portion of the document that will contain any new elements, in our case that may be:

    $('#tblTasks tbody')

We could alternatively say we want to add the event listener to any new elements anywhere in the document with:

    $(document)

Next we specify the type of event listener we want to attach, the type of element we want the event listener added against, and the callback we want executed.

In order to demonstrate this, we will add a click listener to be able to delete each row in the table.

Before beginning, we need to add navigation buttons to each row in the table body. Add the following to each row in the __tbody++ immediately before the </tr> (there are 3 of them):

    <td>
      <nav>
        <a href="#" class="editRow">Edit</a>
        <a href="#" class="completeRow">Complete</a>
        <a href="#" class="deleteRow" >Delete</a>
      </nav>
     </td>

In addition, add a new header cell inside the table header immediately before the </tr>:

    <th>Actions</th>

Finally, to make sure the columns are sized correctly, change the column groups for the table as follows:

    <colgroup>
      <col width="40%">
      <col width="15%">
      <col width="15%">
      <col width="30%">
    </colgroup>

In order to verify the changes, executing the following should return three elements:

    $('.deleteRow')

We can now add an event listener as follows:

    $('#tblTasks tbody').on('click', '.deleteRow',   function(evt) {
        evt.preventDefault();
        $(evt.target).parents('tr').remove();
     });

When an element with the class __deleteRow__ is clicked, this event listener will find the __tr__ element that is a parent of this element:

    $(evt.target).parents('tr')

It will then remove this element from the document using the __remove__ function.

Naturally this works for the three rows that were in the table when the page loaded. If you want to prove that this approach works for rows added directly to the DOM, you can add a new row to the table with the following code:

    $('#tblTasks tbody tr:first' ).clone().insertAfter('#tblTasks tbody tr:last')

This code will select the first row from the table, clone it, to create a new row, and then insert it after the last row in the table. You will be able to then delete this row from the table using its delete button, without having to add an event listener explicitly to the button.

   |   |   |
   |---|---|
   |   |Earlier versions of jQuery used a function called live to add dynamic event listeners. This function has been deprecated and should not be used.|
   |   |   |

So far we have concentrated on click events. There are many other events that can be listened for with jQuery. The following are the other common events, all of which work in the same basic way:

* __dblclick__: is invoked when an element is clicked twice in quick succession.
* __hover__: is invoked when the mouse hovers over the element.
* __mousedown__: is invoked when the mouse button is pressed, and before the button is release.
* __mouseup__: is invoked when the mouse button is released.
* __keypress__: is invoked each time the user types a key into an element, such as a text field.
* __keydown__: is invoked when the user presses a key, but before the output is reflected on screen. This allows you to veto the action with preventDefault.
* __blur__: is invoked when the focus leaves a form field. This is useful when you wish to validate content after the user has finished typing.
* __change__: is invoked when the value of a form field changes.
* __focus__: is invoked when the form field receives focus.

For a complete list of events, see the jQuery documentation.

Before finishing this section, we will make a minor change to ensure that our event handlers are not added before the DOM has been fully constructed. Ideally we want to start processing scripts after the DOM has been constructed, even if all resources (such as images) have not been loaded. Due to the way JavaScript works, it is possible that it will begin processing before the DOM has loaded, in which case elements will not be available when selected:

   |   |   |
   |---|---|
   |   |Technically in our case we do not need to worry about this, since our script is declared at the bottom of the page. It is however a good habit to use the approach suggested below, even in this case.|
   |   |   |

In order to detect that the DOM has fully loaded we can listen for the __ready__ event:

    $(document).ready()
        $('[required="required"]').prev('label').append( '<span>*</span>').children( 'span').addClass('required');
        $('tbody tr:even').addClass('even');
        $('#btnAddTask').click(function(evt) {
            evt.preventDefault();
            $('#taskCreation').removeClass('not');
        });

        $('tbody tr').click(function(evt) {
            $(evt.target).closest('td').siblings( ).andSelf( ).toggleClass( 'rowHighlight');
        });

        $('#tblTasks tbody').on('click', '.deleteRow', function(evt) {
            evt.preventDefault();
            $(evt.target).parents('tr').remove();
        });
    });

If you need to delay code execution until all resources have loaded, the __load__ event can be used instead:

    $(document).load()

# Writing jQuery Plugins

One of the reasons jQuery has become so popular is that it is trivial to write plugins that integrate with jQuery. This has led to a huge number of plugins freely available under the MIT license, and also allows you to write your own custom plugins.

A jQuery plugin usually works by performing an operation on an element, or set of elements returned from a jQuery selection. Just like standard jQuery functions, depending on how the plugin is written it may be capable of acting on a whole set of elements, or just a single element.

In this section we are going to write a plugin that can be executed on a __form__ element that has been selected using jQuery. This plugin will then return an object where the property names on the object are the form field names, and the values are the values of that field. Effectively this plugin is going to serialize the values on a form into an object. We will also allow this plugin to operate in the opposite direction: to de-serialize an object onto a __form__.

This plugin will take advantage of programming by convention. We will assume that the object names and the form field names should always match, even though there will be nothing in the code that insists on this.

Programming by convention does have disadvantages. For instance, if anyone changed the name of a field this will result in changes to the property on the objects serialized from that form, and that may in turn break other code that had expectations about what those properties would be. Programming by convention can significantly reduce the amount of code required to implement functionality however.

Plugins work in jQuery by passing the jQuery function to the plugin function, which will then extend the jQuery function by creating an object with a set of new functions in it.

It is not particularly important that you understand this process, but the boilerplate code for adding new functions to jQuery looks like this:

    (function($) {
        $.fn.extend({
            action: function() {}
        });
    })(jQuery);

In this case we are adding a single new jQuery function called __action__. This could then be invoked as follows:

    > $('div').action()

Inside the function we can use the __this__ variable to access the element or elements that the function has been executed on, for instance in the example above, all the div elements. This will either represent an array of jQuery elements, or a single jQuery element. In our example we are always going to assume that __this__ is a single element.

To begin, we will write a rudimentary version of the serialize function that simply writes the contents of the __form__ to the console log:

    (function($) {
      $.fn.extend({
        toObject: function() {
          console.log(this.serialize());
        }
      });
    })(jQuery);

This implementation adds a new function to jQuery called toObject, and is going to take advantage of a function already available in jQuery that serializes a form into a string.

Add this to the script section of the web page, refresh the web page, and click “Add task”. Enter values into all the fields, and then call:

    > $('form').toObject()

This should print out a text string with the contents of the form.

Now that we have a basic implementation, we can start writing the code needed to return an object with properties populated from the form.

Although jQuery does not have a function for serializing a form into an object, it does have a function for serializing a form to an array. This function returns an array where each form field is represented by an element in the array, and consists of a name and a value. In order to see this function in action, execute the following:

    > $('form').serializeArray()

We will use this as the basis of our implementation, and iterate over the array using a jQuery helper function called __each__:

    $.each($('form').serializeArray(), function(i, v) {

    });

   |   |   |
   |---|---|
   |   |jQuery has a number of utility functions available with “$.” prefixes. Unlike other jQuery functions, these are not used for selecting elements, and they cannot be invoked on a set of elements.|
   |   |   |

This particular function will iterate over an array and pass each index and value to the callback function we provide. To see this in action, try executing the following:

    > $.each([1,4,8,16,32], function(i, v) {
          console.log('index: '+i);
          console.log('value: '+v)
      });

This should print out:
index: 0
value: 1
index: 1
value: 4
index: 2
value: 8
index: 3
value: 16
index: 4
value: 32

Unlike the standard JavaScript __for__ and __while__ loops, the __$.each__ helper has the ability to iterate over both arrays and objects.

Now that the skeleton of __toObject__ is in place, we can complete the implementation as follows:

    (function($) {
      $.fn.extend({
        toObject: function() {
          var result = {}
          $.each(this.serializeArray(), function(i, v) {
              result[v.name] = v.value;
          });
          return result;
        }
      });
    })(jQuery);

If you now execute the following:

    > o = $('form').toObject()

The variable o will contain an object, with properties reflecting the names of the field in the form. It is therefore possible to execute the following:

    > o.task

You will notice that the implementation starts by creating an empty object. Properties are then added to the object for each form element. The implementation uses the [] bracket approach to add properties, rather than the “.” notation. This is important, because the name of fields may not conform to the standards required by JavaScript when using the “.” notation.

Now that we have a __toObject__ function, we can add a second function to de-serialize an object back onto a form. In order to add a second function, we simply create a new property in the object we are creating to extend jQuery. This function will be called __fromObject__ and accepts an object as a parameter:

    (function($) {
      $.fn.extend({
        toObject: function() {
          var result = {}
          $.each(this.serializeArray(), function(i, v) {
            result[v.name] = v.value;
          });
          return result;
        },
        fromObject: function(obj) {

        }
      });
    })(jQuery);

The first task of this function will be to extract all the form fields from the __form__ this function is called on (which again, will be represented by the __this__ variable. We can extract the input fields with the following:

    this.find('input')

The only problem is that this will not include select boxes, since they are not considered types of input fields. Fortunately, jQuery provides a selector that does return all input fields, including select fields:

    this.find(':input')

Once all the form fields are found, the implementation will iterate over all the fields and extract their name attribute. It will then look in the object for a property with that name, and if there is one, it we will set the value of the field from the value of the property:

    fromObject: function(obj) {
      $.each(this.find(':input'), function(i,v) {
        var name = $(v).attr('name');
        if (obj[name]) {
          $(v).val(obj[name]);
        } else {
          $(v).val('');
        }
      });
    }

You will notice that we add the __$()__ construct around the references to __v__. This is because the value returned is a native DOM object; therefore it is necessary to convert them to jQuery objects in order to use the __attr__ method.

With that implementation in place you should be able to change values in the form, and then call the following to repopulate it back to the original values stored in the o variable:

    > $('form').fromObject(o)

The final version of the jQuery plugin is as follows:

    (function($) {
      $.fn.extend({
        toObject: function() {
          var result = {}
          $.each(this.serializeArray(), function(i, v) {
            result[v.name] = v.value;
          });
          return result;
          },
        fromObject: function(obj) {
          $.each(this.find(':input'), function(i,v) {
            var name = $(v).attr('name');
            if (obj[name]) {
              $(v).val(obj[name]);
            } else {
              $(v).val('');
            }
          });
        }
      });
    })(jQuery);

# Using existing plugins

Before writing your own plugin, it is useful to check if any plugins are already available that meet your needs. There is a vast library of plugins available on the Internet. Some are well supported and widely used; others are unsupported, or used by a handful of people.

Most plugins are available under the MIT license, meaning you are free to modify them in any way you need.

In this section we are going to use a plugin for generating HTML from a template. The plugin we will use is jQuery Template, and is available here:

https://github.com/BorisMoore/jquery-tmpl

You can choose to download either jquery.tmpl.js or jquery.tmpl.min.js.

Alternatively, you can use the following CDN version:
http://ajax.aspnetcdn.com/ajax/jquery.templates/beta1/jquery.tmpl.js

   |   |   |
   |---|---|
   |   |When a library has .min in its name, it is exactly the same as the one without it, but has been compressed. It is common to compress JavaScript files to improve download speed, but some people (mistakenly) also see it as a way to add obfuscation to their code to stop it being copied.|
   |   |If you would like to investigate this subject further, or compress your own files, see this website:|
   |   |https://developers.google.com/speed/articles/compressing-javascript|
   |   |   |

This plugin was originally intended to form part of the core jQuery library, but these plans have not come to fruition. The library is now largely unsupported, but is still a useful templating library, and will be used here primarily to demonstrate the use of a jQuery plugin.

If you would like to use a supported templating library on a project, I recommend the Underscore library, which provides templating functionality that performs essentially the same role.

In order to use a downloaded version of jQuery Template, first copy it to the scripts folder of the project. Once in place, add the following to the head section of the page, but after the main jQuery import:

    <head>
    <meta charset="utf-8">
    <title>Task list</title>
    <link rel="stylesheet" type="text/css" href="styles/tasks.css" media="screen" />

    <script src="http://ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

    <!-- starting new -->
    <script src="scripts/jquery-tmpl.js"></script>
    <!-- ending new -->

    </head>

   |   |   |
   |---|---|
   |   |You may notice that it is no longer necessary to specify that the language of a script file is “text/javascript”. HTML5 assumes by default that scripts are JavaScript.|
   |   |   |

This is all that is required in order to start using the jQuery Template plugin. When the script loads it will automatically add new features to jQuery, just as our own custom plugin added new features to jQuery.

When new tasks are created via the form, we need to dynamically add them to the __table__; this means creating a new __tr__ element in the table, and adding the appropriate __td__ columns.

We could achieve this with jQuery directly by generating a string to represent the HTML and then appending it to the table. As we saw earlier in this chapter, it is possible to generate elements directly out of HTML and add them into the DOM.

Constructing HTML within code is error prone however, and it would be more convenient if we can write the basic structure of the row as HTML, and leave placeholders for the dynamic content.

   |   |   |
   |---|---|
   |   |Templating libraries are widely used in software development. Like jQuery template, they provide basic control structures such as loops and branching, and allow placeholders for parameters.|
   |   |   |

jQuery template allows us to define the following template in the HTML page:

    <script id="taskRow" type="text/x-jQuery-tmpl">
    <tr>
      <td>${task}</td>
      <td><time datetime="${requiredBy}"> ${requiredBy} </time></td>
      <td>${category}</td>
      <td>
        <nav>
          <a href="#">Edit</a>
          <a href="#">Complete</a>
          <a href="#" class="deleteRow">Delete</a>
        </nav>
      </td>
    </tr>
    </script>

This can be added at the very bottom of the page, before the </html> (not inside the other __script__ block). Note that this is essentially just a block of HTML, except it contains placeholders for values. The placeholders are inside the following constructs: __${}__.

Also note that this is not a standard JavaScript block, since it is defined as type __text/x-jQuery-tmpl__. The block also contains an ID, which is not typically needed in standard script blocks.

We now are going to implement a rudimentary version of the save functionality. Start by adding an ID to the save button:

    <a href="#" id="saveTask">Save task</a>

Next, add a __click__ event listener to the save task button. This is going to convert the form data into an object using the plugin we developed in the last section. It is then going to pass this object to the template we constructed above. Notice that in the template the placeholder names match the property names that will appear on our task object.

The template will generate a block of HTML, which we will then append to the table body. Add the following code to the __script__ section of tasks2.html alongside the other event handlers:

    $('#saveTask').click(function(evt) {
      evt.preventDefault();
      var task = $('form').toObject();
      $('#taskRow').tmpl(task).appendTo($('#tblTasks tbody'));
    });

As you can see, two lines of code are sufficient to convert the form to an object, and include the contents in the __table__, and this could be condensed to one line with relative ease.

As stated above, this is a rudimentary version of the save functionality. For instance, it does not contain any validation; therefore you can add invalid data to the table. This, and other minor issues, will be fixed once we start to turn this into a true web application in a couple of chapters time.

Now that the save is implemented we can remove the three rows that were added to the table by default each time the page was loaded, and add rows using the “Add task” and “Save task” functionality. In addition, the rows added should be able to be deleted using the “Delete task” option.

The tasks2.html page should now contain the following markup:

    <!DOCTYPE html>
    <html lang="en">
    <head>
    <meta charset="utf-8">
    <title>Task list</title>
    <link rel="stylesheet" type="text/css"     href="styles/tasks.css"
        media="screen" />
    <script src="scripts/jquery-2.0.3.js"></script>
    <script src="scripts/jquery-tmpl.js"></script>
    </head>
    <body>
      <header>
        <span>Task list</span>
      </header>
      <main>
        <section id="taskCreation" class="not">
          <form>
            <div>
              <label>Task</label>
              <input type="text" required="required"
                     name="task" class="large"
                     placeholder="Breakfast at Tiffanys" />
             </div>
             <div>
               <label>Required by</label>
               <input type="date" required="required"
                        name="requiredBy" />
              </div>
              <div>
                <label>Category</label>
                <select name="category">
                  <option     value="Personal">Personal</option>
                  <option     value="Work">Work</option>
                </select>
               </div>
               <nav>
                  <a href="#" id="saveTask">Save task</a>
                  <a href="#">Clear task</a>
                </nav>
            </form>
        </section>
        <section>
            <table id="tblTasks">
                <colgroup>
                    <col width="40%">
                    <col width="15%">
                    <col width="15%">
                    <col width="30%">
                </colgroup>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Due</th>
                        <th>Category</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                </tbody>
            </table>
            <nav>
                <a href="#" id="btnAddTask">Add task</a>
            </nav>
        </section>
        </main>
        <footer>You have 3 tasks</footer>
    </body>
    <script>
    $(document).ready(function() {
        $('[required="required"]').prev('label').append( '<span>*</span>').children( 'span').addClass    ('required');
        $('tbody tr:even').addClass('even');
        $('#btnAddTask').click(function(evt) {
            evt.preventDefault();
            $('#taskCreation').removeClass('not');
        });
        $('tbody tr').click(function(evt) {
            $(evt.target).closest('td' ).siblings(     ).andSelf( ).toggleClass( 'rowHighlight');
        });

        $('#tblTasks tbody').on('click', '.deleteRow',     function(evt) {
            evt.preventDefault();
            $(evt.target).parents('tr').remove();
        });

        $('#saveTask').click(function(evt) {
            evt.preventDefault();
            var task = $('form').toObject();
            $('#taskRow').tmpl(task).appendTo( $    ('#tblTasks tbody'));
        });
    });

    (function($) {
      $.fn.extend({
        toObject: function() {
          var result = {}
          $.each(this.serializeArray(), function(i, v) {
            result[v.name] = v.value;
          });
          return result;
        },
        fromObject: function(obj) {
          $.each(this.find(':input'), function(i,v) {
              var name = $(v).attr('name');
              if (obj[name]) {
                $(v).val(obj[name]);
               } else {
                 $(v).val('');
               }
             });
           }
        });
    })(jQuery);
    </script>

    <script id="taskRow" type="text/x-jQuery-tmpl">
    <tr>
      <td>${task}</td>
      <td><time datetime="${requiredBy}">     ${requiredBy}</time></td>
      <td>${category}</td>
      <td>
        <nav>
          <a href="#">Edit</a>
          <a href="#">Complete</a>
          <a href="#" class="deleteRow">Delete</a>
        </nav>
      </td>
    </tr>
    </script>

    </html>

# Conclusion

This chapter has introduced all the important aspects of jQuery that deal with DOM manipulation. As has been demonstrated, jQuery provides an elegant and concise set of function calls for selecting, traversing and manipulating the DOM, along with adding event listeners.

Although jQuery does not do anything that could not be done natively with the DOM API (or other libraries such as Dojo for that matter), jQuery provides the following benefits:

* It takes care of any quirks that may exist in different versions of web browsers.
* It uses the same basic set of selectors as CSS, meaning anyone who understands CSS can quickly adapt to jQuery.
* It provides a concise and intuitive set of function calls that are easy to learn, and easy to use in conjunction with one another.
* It is easy to extend jQuery to solve new problems.
* jQuery is widely used, therefore there is a wealth of information and help available online.

There are several aspects of jQuery that have not been examined as yet. Foremost amongst these are the AJAX API which will be introduced later in this book. Several other jQuery topics will be introduced at the appropriate point in the book.
# Best practices

## Example: A date screenfield will change value when the user fills in a return code screenfield
In this exmaple the user will fill in the return code for the transmittal. The following actions are sequentially required to properly process the request.
* get the return code from the screen.
* validate the return code
* get the date
* fill in the date
* refresh the screen

Given: 
* 1 return code screenfield. The return code screenfield has a LOV lookup attached that will validate the give value on the server.
* 1 date screenfield. This field is based on the JQuery datepicker. (add URL) 

We need to retrieve the return code value from the screenfield after the user inputs the value. This means that we need to listen to the onChange event for the return code screenfield. Because we can only have a single onChange event attached to the ACDC object (Framework limitation), and this onChange event is already being used by the LOV/validation action. We need to add a JQuery onChange listeren. Because we are using JQuery, the HTML objects needs to exists to be able to access is. This mean we need to add the onChange event in the post\_dialog\_create [hook](handler_details).

This is done like so:

	Add the on('change', doStuff)
	
Now that have retrieved the value, we need to query the database to retrieve the next generated date.

	DwrGeneral.queryForDFate(return_code, set_date)
	
With the retrieved date we can set the date on screen:

	 function set_dqate(){
	 	setThaDate()
	 };


## Example: Customizing a handler
##  
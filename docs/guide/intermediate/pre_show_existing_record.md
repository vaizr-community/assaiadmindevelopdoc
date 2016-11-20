# pre\_show\_existing\_record

Values is an in/out parameter that can be used to get or set data. The values are used to show in the screen if they are defined in options.pageBodyItems eg. mainFields.

Get:

	var parameters = {};	
	parameters.ljob_seq_nr = values.ljob_seq_nr;
	
Set:

	values.unit = selectedRecord.asat_unit;

This is used when the selectedRecord contains more columns then the database rectype. The selectedRecord is based on the rectype_search.psql which can have joined table columns. To show them in the screen you create the page items and assign the selectedRecord value to it through values.item = selectedRecord.column_x

Other code examples:


	    $.alfa.DlgLov.disableLov(classField.id);
	   detailsContext.enableItems(['asset_item_tree', 'set_project', 'reset_atttributes']);
	    _enableButtons(pageItems, ['checkout']);
	   $('#' + mainFields.data.asst_seq_nr.id + '_display').prop("disabled", true);
	    $('#' + mainFields.data.asst_seq_nr.id  + '_display').addClass('displayonly');
	    $('#' + mainFields.data.asst_seq_nr.id  + '_lov').hide();
	    mainFields.data.asty_seq_nr.service.parameters.inmo_seq_nr = selectedRecord.inmo_seq_nr;
	   $('#' + calcButton_id).button('enable');

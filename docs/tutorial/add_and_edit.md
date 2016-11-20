# Tutorial 5 : Walk through add and edit

# Introduction


This we do by hitting the `Add` button. Let's see in the code what happens. First we have to find the Add button in the code. This add button is part of the StandardDetailTabHandler. In the file `/ScottTiger/src/main/webapp/js/details/handlers/handler_st2_docs.js` we find the following line of code

            var tabHandler = new Assai.StandardDetailTabHandler(options);

Drilling in on `Assai.StandardDetailTabHandler(options)` we get to the file `../ScottTiger/src/main/webapp/js/details/standard_detail_tab.js`

and in this file we find back the following line

            ctxOptions.menuFunctions.add = _add;

With other words. If you push the button `Add`. the function `_add` is executed. Below you find the code of function `_add`

    function _add(items, item) {
        showDetailsPopup(dialogId, className, clas_seq_nr, masterRecord, null, $.alfa.alfaUtils.getLabel("add_" + recName), false, tabContext, extraOptions);
    }

The call to `showDetailsPopup` brings us back to the showDetailsPopup function in `/ScottTiger/src/main/webapp/js/details/handlers/handler_st2_docs.js`


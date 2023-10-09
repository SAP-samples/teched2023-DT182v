# Create an SAP BTP ABAP Environment Trial User

In this exercise, you will create a trial user in the SAP BTP, ABAP Environment. 

If you have not already done so you have first to register for the SAP BTP Trial [here].(https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html).

The steps you you to activate the ABAP Environment in the SAP BTP trial by creating an appropriate user have have been described in the following tutorial.

[Create an SAP BTP ABAP Environment Trial User](https://developers.sap.com/tutorials/abap-environment-trial-onboarding.html)

## Level 2 Heading

After completing these steps you will have....

1.	Click here.
<br>![](/exercises/ex0/images/00_00_0010.png)

2.	Insert this code.
``` abap
 DATA(params) = request->get_form_fields(  ).
 READ TABLE params REFERENCE INTO DATA(param) WITH KEY name = 'cmd'.
  IF sy-subrc <> 0.
    response->set_status( i_code = 400
                     i_reason = 'Bad request').
    RETURN.
  ENDIF.
```

## Summary

Now that you have ... 
Continue to - [Exercise 1 - Exercise 1 Description](../ex1/README.md)

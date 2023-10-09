# Exercise 2 - Behavior extension

In this exercise, we will create...


## Exercise 2.1 Add validations 

After completing these steps you will have created a validation to check the delivery date.

```abap
validation zz_validateDeliverydate on save { create;   field DeliveryDate; }

extend draft determine action Prepare
  {
    validation zz_validateDeliveryDate;

  }

```


## Exercise 2.2 Add determinations

```abap
determination ZZ_setOverallStatus on modify {  field OrderedItem; }
determination ZZ_fillnotes on modify { field overallstatus; }
```

## Exercise 2.3 Add side effects

```abap
side effects { field OverallStatus affects field Notes ; }
```


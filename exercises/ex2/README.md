# Exercise 2 - Extend the extensible RAP BO

In this exercise, we will create...

## Exercise 2.1 - Extend the behavior

### Exercise 2.1.1 Add validations 

After completing these steps you will have created a validation to check the delivery date.

```abap
validation zz_validateDeliverydate on save { create;   field DeliveryDate; }

extend draft determine action Prepare
  {
    validation zz_validateDeliveryDate;

  }

```


### Exercise 2.1.2 Add determinations

```abap
determination ZZ_setOverallStatus on modify {  field OrderedItem; }
determination ZZ_fillnotes on modify { field overallstatus; }
```

### Exercise 2.1.3 Add side effects

```abap
side effects { field OverallStatus affects field Notes ; }
```

## Exercise 2.2 - Extend the data model

### Exercise 2.2.1 - Add a field to the extension include

```abap
  zz_feedback_zaa : abap.char(256);
```

### Exercise 2.2.x - Add extensions for R-view
### Exercise 2.2.x - Add extensions for i-view
### Exercise 2.2.x - Add extensions for c-view
### Exercise 2.2.x - Add extensions for e-view
### Exercise 2.2.x - Add extensions for draft query view


.... 

### Exercise 2.2.x - Add an action and instance feature control

```abap
field(features : instance) zz_feedback_zaa;
action(authorization : global,
//       authorization : instance,
            features : instance ) ZZ_ProvideFeedback  parameter zabs_feedback result[1] $self;
```

After completing these steps you will have...

### Exercise 2.2.x - Add use statement in projection BDEF

## Summary

You've now ...

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)

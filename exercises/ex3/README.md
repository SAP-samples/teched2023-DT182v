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


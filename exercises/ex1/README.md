# Exercise 1 - Generate an extensible RAP BO

In this exercise, we will generate an extensible RAP BO. Since extending a RAP BO in parallel by several developers can cause severe problems every participant will work with his or her own base RAP BO.


## Exercise 1.1 - Generate RAP BO

After completing these steps you will have created an extensible RAP Business Object.

1. Right-click **Favorite Objects** and click **Add Object**.
   
2. Search for **`ZDMO_GEN_RAP630_SINGLE`**, select it and click **OK**.    

3. Right-click **`ZDMO_GEN_RAP630_SINGLE`**, select **Run As** > **ABAP Application (Console) F9**.

4. Now your packages are created. Check the ABAP console. **⚠Copy the package names and the suffix for later use.**

## Exercise 1.2 - Adapt the generated RAP BO

### Adapt include structure

We have to adapt the generated include structure. This is because the XCO libraries currently to not yet support generating some of the needed annations.

<pre>
@EndUserText.label : 'Extension include for Shop'
@AbapCatalog.enhancement.category : #NOT_EXTENSIBLE
define structure zrap630sshop_05b {

  dummy_field : abap.char(1);

}
</pre>

Change the enhancement category such that table gets the category

<pre>
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
</pre>

Then add these annotations that are needed in order to make the generated inlcude structure extensible: 

<pre>
@AbapCatalog.enhancement.fieldSuffix : 'ZAA'
@AbapCatalog.enhancement.quotaMaximumFields : 350
@AbapCatalog.enhancement.quotaMaximumBytes : 3500
@AbapCatalog.enhancement.quotaShareCustomer : 50
@AbapCatalog.enhancement.quotaSharePartner : 50
</pre>

### Adapt the table

Open the generated table `zrap630_ashop###` and change the enhancement category to the value `extensible_any`. 

<pre>
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
</pre>

### Adapt the draft table

Perform the same change for the draft table `zrap630sh00d_###` and change the enhancement category to the value `extensible_any`. 

<pre>
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
</pre>

## Summary

You've now ...

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)


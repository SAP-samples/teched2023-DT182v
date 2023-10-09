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

We have to adapt the generated include structure. This is because the XCO libraries currently to not yet support generating some of the annotions that are needed for the include structure used by an extensible entity of an extensible RAP business object.

1. Change the enhancement category such that table gets the category   

   <pre>
   @AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
   </pre>

2. Then add these annotations that are needed in order to make the generated inlcude structure extensible:  

   <pre>
   @AbapCatalog.enhancement.fieldSuffix : 'ZAA'
   @AbapCatalog.enhancement.quotaMaximumFields : 350
   @AbapCatalog.enhancement.quotaMaximumBytes : 3500
   @AbapCatalog.enhancement.quotaShareCustomer : 50
   @AbapCatalog.enhancement.quotaSharePartner : 50
   </pre>

The code of the extension include should now look like as follows :

<pre>
@EndUserText.label : 'Extension include for Shop'
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
@AbapCatalog.enhancement.fieldSuffix : 'ZAA'
@AbapCatalog.enhancement.quotaMaximumFields : 350
@AbapCatalog.enhancement.quotaMaximumBytes : 3500
@AbapCatalog.enhancement.quotaShareCustomer : 50
@AbapCatalog.enhancement.quotaSharePartner : 50
define structure zrap630sshop_### {

  dummy_field : abap.char(1);

}
</pre>

### Adapt the table

Open the generated table `zrap630_ashop###` and change the enhancement category to the value `extensible_any`. 

<pre>
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
</pre>

The source code of your table should now read as follows:   

<pre>
@EndUserText.label : ' Table for entity ZRAP630R_ShopTP_###'
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
@AbapCatalog.tableCategory : #TRANSPARENT
@AbapCatalog.deliveryClass : #A
@AbapCatalog.dataMaintenance : #NOT_ALLOWED
define table zrap630_ashop### {

  key mandt             : abap.clnt not null;
  key order_uuid        : sysuuid_x16 not null;
  order_id              : ad_persnum;
  ordered_item          : abap.char(40);
  currency_code         : abap.cuky;
  @Semantics.amount.currencyCode : 'zrap630_ashop###.currency_code'
  order_item_price      : abap.curr(11,2) not null;
  delivery_date         : abap.dats;
  overall_status        : abap.char(30);
  notes                 : abap.char(256);
  last_changed_at       : abp_lastchange_tstmpl;
  created_by            : abp_creation_user;
  created_at            : abp_creation_tstmpl;
  local_last_changed_by : abp_locinst_lastchange_user;
  local_last_changed_at : abp_locinst_lastchange_tstmpl;
  include zrap630sshop_###;

}
</pre>

### Adapt the draft table

Perform the same change for the draft table `zrap630sh00d_###` and change the enhancement category to the value `extensible_any`. 

<pre>
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
</pre>

The source code of your draft table `zrap630sh00d_###` should now read as follows:   

<pre>
@EndUserText.label : ' Draft table for entity ZRAP630R_ShopTP_###'
@AbapCatalog.enhancement.category : #EXTENSIBLE_ANY
@AbapCatalog.tableCategory : #TRANSPARENT
@AbapCatalog.deliveryClass : #A
@AbapCatalog.dataMaintenance : #NOT_ALLOWED
define table zrap630sh00d_### {

  key mandt          : abap.clnt not null;
  key orderuuid      : sysuuid_x16 not null;
  orderid            : ad_persnum;
  ordereditem        : abap.char(40);
  currencycode       : abap.cuky;
  @Semantics.amount.currencyCode : 'zrap630sh00d_###.currencycode'
  orderitemprice     : abap.curr(11,2);
  deliverydate       : abap.dats;
  overallstatus      : abap.char(30);
  notes              : abap.char(256);
  lastchangedat      : abp_lastchange_tstmpl;
  createdby          : abp_creation_user;
  createdat          : abp_creation_tstmpl;
  locallastchangedby : abp_locinst_lastchange_user;
  locallastchangedat : abp_locinst_lastchange_tstmpl;
  "%admin"           : include sych_bdl_draft_admin_inc;
  include zrap630sshop_###;

}
</pre>

### Adapt the generated projection view 

Open the generated projection Behavior defintion `ZRAP630C_ShopTP_###`. Here we have to add the statement `use side effects;`. This is because this statement cannot be added by the extension and has to be part of the base business object. 

Unfortunately it will only become possible to generated this code statement in the upcoming _2402-release_ of the ABAP Environment.

The code of the generated projection behavior definition should now read as follows.    

<pre>
projection;
strict ( 2 );
extensible;
use draft;
use side effects;
define behavior for ZRAP630C_ShopTP_### alias Shop
extensible
use etag

{
  use create;
  use update;
  use delete;

  use action Edit;
  use action Activate;
  use action Discard;
  use action Resume;
  use action Prepare;
}   
</pre>

## Summary

You've now ...

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)


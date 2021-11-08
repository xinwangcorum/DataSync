# Catalog Maintenance

**Use case:**

- A head office would like to update the name of a brand, based on an Id.

```json
Brand: {
   "Action":"AddBrand", //AddBrand, AddUpdateBrand, DeleteBrand
   "Brand":{
      "Id":"GC",
      "Name":"Gucci"
   }
}
```

 

**Use case:**

- A head office would like to merge two brands, specifically merging one brand into another brand.

```json
Brand: {
   "Action":"MergeBrand", //MergeBrand, //UpdateBrand
   "FromBrand":{
      "Id":"GCA",
      "Name":"Gucci Australia"
   },
   "ToBrand":{
      "Id":"GC",
      "Name":"Gucci"
   }
}
```

 

This pattern is replicated for each: 

- Brand
- Grade
- Manufacturer
- Supplier

 

**Use case: Merchandise Hierarchy**

- A head office would like to merge two brands, specifically merging one heirarchy level into another hierarchy level.

```json
MerchandiseHierarchy: {
   "Action":"UpdateHierarchy",
   "FromMerchandiseHierarchy":{
      "Level":"Department",
      "Value":"Clothing"
   },
   "ToMerchandiseHierarchy":{
      "Level":"SubDepartment",
      "Value":"Apparel"
   }
}
```

 

**Use case: Move Merchandise Hierarchy**

- A head office would like to move a child hierarchy to another hierarchy

```json
MerchandiseHierarchy: {
   "Action":"UpdateParentHierarchy",
   "MerchandiseHierarchy":{
      "Level":"SubDepartment",
      "Value":"Mens clothing"
   },
   "FromParentMerchandiseHierarchy":{
      "Level":"Department",
      "Value":"Clothing"
   },
   "FromParentToMerchandiseHierarchy":{
      "Level":"Department",
      "Value":"Apparel"
   }
}
```

 

**Use case: Update Supplier Information**

```json
  "SupplierInformation": [
  {
    "Action": "UpdateSupplierInformation"
    "Supplier": {
     "ID" : "113",
     "Name": "High fashion supply co."
    },
    "Description": "Farmer T-Shirt (Red)",
    "StoreOrderAllowedFlag": true,
    "SupplierItemID": "ASDX123Z",
    "SalesUnitPerPackUnitQuantity": 1,
    "CurrentPrice": [
        {
          "ValueTypeCode": "UnitCostPrice",
          "Value": "179.00",
          "PriceRules": [
            {
              "Eligibility": {
                "ThresholdQuantity": {
                  "Units": 5,
                  "UnitOfMeasureCode": "EA"
                }
              },
              EffectiveDateTimestamp: "2020-01-01",
              ExpirationDateTimestamp: "2021-02-02"
            }
          ]
        },
        {
          "ValueTypeCode": "RegularSalesUnitPrice",
          "Value": "199.00"
        }
      ],
    }
  ]
}
```

 
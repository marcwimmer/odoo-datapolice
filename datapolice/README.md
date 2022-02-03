# datapolice

## Using a python def for checking

```xml
<record model="data.police" id="products1">
  <field name="model">product.product</field>
  <field name="checkdef">check_incoming_noproduction_nopicking</field>
  <field name="name">Incoming stock moves, that have no production or picking-in</field>
</record>
```

```python
def datapolice_check_same_lot_type(self):
    if self.origin_sales and self.matching_prod_product_ids:
        if not self.lot_type == self.matching_prod_product_ids:
            return False # can return also a string!
    elif (self.origin_buy or self.origin_buy) and self.matching_sales_product_ids:
        if not self.lot_type == self.matching_sales_product_ids:
            return False
    # return True if happy
    return True
```

## Using expression in xml to check (xml-only)

```xml
<record model="data.police" id="products1">
  <field name="model">product.product</field>
  <field name="name">Incoming stock moves, that have no production or picking-in</field>
  <!-- Define the happy situation -->
  <field name="expr">obj.name != 'not allowed'</field>
</record>
```


## Contributors

* Marc Wimmer <marc@itewimmer.de>

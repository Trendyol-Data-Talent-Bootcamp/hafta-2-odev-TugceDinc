# Soru 4)

```sql
merge tugce_dinc.content_category cc -- Target table
using tugce_dinc.content_category_20201222_00_59 cc2 -- Source table
on cc.id = cc2.id
when not matched by target then
  Insert (cdc_date, is_deleted,id,category)
  values (cc2.cdc_date, cc2.is_deleted, cc2.id, cc2.category)
when matched and farm_fingerprint(to_json_string(cc)) <> farm_fingerprint(to_json_string(cc2)) then
  Update set
        cc.is_deleted = cc2.is_deleted,
        cc.cdc_date = cc2.cdc_date,
        cc.category = cc2.category
when not matched by source then
  Update set cc.is_deleted = true

```

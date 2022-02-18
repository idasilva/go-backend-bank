# go-backend-bank



## Database schema
```
Table accounts as A {
  id bigserial [pk]
  owner varchar [not null]
  balance  bigint [not null]
  currency varchar [not null]
  created_at timestamptz [not null,default: `now()`]
  
  indexes{
    owner
  }
  
}

Table entries {
  id bigserial [pk]
  account_id bigint [ref: > A.id]
  amount  bigint [not null, note:"can be positive or negative"]
  created_at timestamptz [not null,default: `now()`]
    indexes{
    account_id 
  }
 }
 
 
Table transfers {
  id bigserial [pk]
  from_account_id bigint [ref: > A.id]
  to_account_id bigint [ref: > A.id]
  amount  bigint [not null, note:"must be positive"]
  created_at timestamptz [default: `now()`]
      indexes{
    from_account_id
    to_account_id
    (  from_account_id,to_account_id)
  }
}
```





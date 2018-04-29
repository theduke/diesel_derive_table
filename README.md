# diesel_derive_table

This crates provides additional derive functionality for [Diesel][diesel],
an ORM for Rust.

## Why

Diesel requires you to either infer the schema from the database, dump the
database to schema definitions with a CLI command, or specify table schemas
with the `table!` macro.

Non of those options really suit my workflow.

This crate contains one custom_derive implementation, `#derive[(Table)]`.

It gives you the ability to define a struct for your table, and also auto-generate
the table! macro for diesel.

## How to use

```rust
#[macro_use] extern crate diesel_derive_table

#[derive(Table, Queryable, AsChangeset, Insertable, Identifiable)]
#[table_name="reddit_posts"]
#[primary_key(uuid)]
pub struct RedditPost {
    #[column_type="Text"]
    #[column_name="my_uuid"]
    pub uuid: String,
    #[column_type="BigInt"]
    pub created_at: i64,
}
```

Notes:

* It supports Diesel's attributes (column_name, table_name, primary_key)
* provides additional attribute `column_type` for specifying the DB column type
* Requires you to specify additional derives, so you stay in control of what
  should be derived.


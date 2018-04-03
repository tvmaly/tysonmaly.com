---
author: admintm
categories:
- Go
date: "2017-04-27T00:28:13Z"
guid: http://www.tysonmaly.com/?p=217
id: 217
title: Go sql examples
url: /programming/go/go-sql-examples/
---

# Go sql examples using sqlx

Assume you have two models a type Business and a type Widget in a one to many relationship.

I want to demonstrate two ways that you can load the widgets into a business object using sqlx.  I am using postgresql.

<pre>package models

import (
    "database/sql"
    "github.com/jmoiron/sqlx"
    "github.com/pkg/errors"
    "time"
)</pre>

<pre>type Business struct {
    Id                int64          `db:"id" json:"id"`
    Name              string         `db:"name" json:"name"`
    Website           sql.NullString `db:"website" json:"website"`
    Created           time.Time      `db:"created" json:"created"`
    Widgets           []Widget        `json:"widgets"`
    CreatedBy         int64          `db:"created_by" json:"created_by"`
}

</pre>

<pre><span class="content">type Widget struct {
    Id          int64          `db:"id" json:"id"`
    Name        string         `db:"name" json:"name"`
    BusinessId  int64          `db:"business_id" json:"business_id"`
}


func (b *Business) Select(db *sqlx.DB, id int64) error {
    return db.Get(b, "select * from business where id = $1", id)
}

// version 1
func (b *Business) GetWidget1(db *sqlx.DB) error {

    err := db.Select(&b.Widgets, "SELECT * FROM widget WHERE business_id = $1", b.Id)

    if err != nil {
        return err
    }

    return nil

}

If you need more control over the process
</span></pre>

<pre><span class="content">// version 2
func (b *Business) GetWidget2(db *sqlx.DB) error {

        rows, err := db.Queryx("SELECT * FROM widget where business_id = $1", b.Id)

        for rows.Next() {

            w := Widget{}

            err = rows.StructScan(&w)

            if err != nil {
                return err
            }

            b.Widgets = append(b.Widgets, w)
        }


}
</span></pre>

<pre><span class="content">

</span></pre>
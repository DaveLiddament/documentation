Filtering
=========

In addition to per-field configuration, each field can be assigned a set of validators and filters.
`Laminas\InputFilter\InputFilter` runs filters before validators, giving you the opportunity to
"cleanup" and normalize data.

The [Laminas\Filter](https://docs.laminas.dev/laminas-filter/) component is
used  to accomplish the filtering phase of content validation.

Here is a list of the available filters:

- [Filter documentation](https://docs.laminas.dev/laminas-filter/)

Filters are executed prior to validation, allowing you to perform normalization tasks.

In this example we'll add a `StringTrim` filter to the name field. To add a filter for a specific
field you need to click on the plus (+) button on the "filter" column:

![Content Validation Filtering Setup](/asset/api-tools-documentation/img/content-validation-filtering-setup.jpg)

Once this is in place, we'll issue a request to the contact service that looks like this:

```HTTP
POST /contact HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8

{
    "age": "34",
    "email": "ralph@rs.com",
    "name": " Ralph Schindler "
}
```

And the response:

```HTTP
HTTP/1.1 201 Created
Content-Type: application/hal+json
Location: http://localhost:8000/contact/5

{
    "_links": {
        "self": {
            "href": "http://localhost:8000/contact/5"
        }
    },
    "age": "34",
    "email": "ralph@rs.com",
    "id": 5,
    "name": "Ralph Schindler",
    "notes": null
}
```

As you will notice, `name` was provided with leading and trailing whitespace, but the response field
does not contain the whitespace.

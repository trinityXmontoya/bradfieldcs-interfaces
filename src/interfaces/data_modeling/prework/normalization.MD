##Database Normalization

Notes from http://www.bkent.net/Doc/simple5.htm

__1.__ Each record of a given type must have the same # of fields.


__2.__ When you have a composite key, a non-key field must contain data that relates to the *entire* key.

Ex. A key `tenant|house` should not contain fields with data only about a `house`, ex. `house_address`. This can lead to issues like:
- duplicating information about the same `house_address` across multiple `tenant|house`s
- having to update `tenant|house` if information about a `house_address` changes (which can lead to stale/conflicting data if not
every required reference is updated)
- if there are no `tenant|house`s, we don't have anywhere to store information about `house_address`es

A solution is to have another key just for `house` which contains a `house_address` field.


__3.__ A non-key field should not contain information about another non-key field

Ex. A key `tenant` should not have fields for `house` and `house_address`


__4.__ A record type should not contain more than one "independent multi-valued" data about an entity.

Ex. A `tenant` can have several `pet`s and several `car`s. If we store the information as one record type i.e. `tenant|house|car`,
we will run into storage + maintenance issues like:
- How do we store a tenant with multiple cars or houses?
- Does a blank `pet/car` mean they don't have one? Or it hasn't been
recorded yet? Or perhaps the information is in another record?
- This will lead to obvious issues when trying to update or delete data.

|tenant|pet         |car     |
|------|------------|--------|
|Nancy |dog         | Benz   |
|Nancy |            | Mustang|
|Nancy |cat         |        |

Re: "independence" -> `pet` and `car` have no direct connection and should therefore not be comingled in this one record type.

__5.__ A record cannot be decomposed into smaller information-preserving records.
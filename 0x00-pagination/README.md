Most endpoints that returns a list of entities will need to have some sort of pagination.

Without pagination, a simple search could return millions or even billions of hits causing extraneous network traffic.

Paging requires an implied ordering. By default this may be the item’s unique identifier, but can be other ordered fields such as a created date.

Offset PaginationPermalink
This is the simplest form of paging. Limit/Offset became popular with apps using SQL databases which already have LIMIT and OFFSET as part of the SQL SELECT Syntax. Very little business logic is required to implement Limit/Offset paging.

Limit/Offset Paging would look like GET /items?limit=20&offset=100. This query would return the 20 rows starting with the 100th row.

ExamplePermalink
(Assume the query is ordered by created date descending)

Client makes request for most recent items: GET /items?limit=20
On scroll/next page, client makes second request GET /items?limit=20&offset=20
On scroll/next page, client makes third request GET /items?limit=20&offset=40
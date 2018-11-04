# Elasticache

An in-memory caching layer which is typically installed to house the `top X number of queries against a database`, which are commonly run and generate a large performance penalty. Adding the data from those queries in a caching layer allows the app to quickly retrieve the results from there, instead of having to ask the database for it each time.
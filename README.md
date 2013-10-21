# Lever Postings API

This repository contains documentation and example apps for the lever postings
REST API. The API is designed to help you make a jobs site. This API is still
quite new and its probably missing some important features. If you need any
features which are missing in this API or find any issues, please email us at
[team@lever.co](mailto:support@lever.co) or file an issue on this repository.

You do not need to use this API to get started with lever job postings. All
published job postings are also automatically viewable via
`jobs.lever.co/yoursite`, for example
[jobs.lever.co/lever](https://jobs.lever.co/lever)

### This API lets you:

- Get paginated job postings for your company
- Get job postings which match particular queries
- Get individual job postings


### The API does not:

- Let you write a custom job posting form, or programatically apply for any of
the postings. If this feature is important to you, please let us know and we
will prioritize it. You should link to `posting.applyUrl` which is at
[jobs.lever.co/site/postingId/apply](https://jobs.lever.co/lever/f6eb3fa6-0ba5-4178-b1ae-e4e0448ba175/apply).
- Let you do full-text searches over open jobs

Note that all jobs posted to lever are currently publically viewable. Internal-only job postings is on our roadmap but not implemented yet.


# API Methods

The API is [RESTful](http://www.infoq.com/articles/rest-introduction) and all
responses are serialized [JSON](http://json.org/).

All API methods are exposed under `api.lever.co/v0/postings/`.

### Sites

All job postings are namespaced within a unique site name. Each company
currently only has one site (usually your company name with no spaces). For
example, Lever's job postings are under the site name `lever`, so they appear
at [https://api.lever.co/v0/postings/lever](https://api.lever.co/v0/postings/lever)
or [https://jobs.lever.co/lever/](https://jobs.lever.co/lever/).


## GET all job postings

> GET /v0/postings/SITE?skip=X&limit=Y

Example [https://api.lever.co/v0/postings/lever?skip=1&limit=3](https://api.lever.co/v0/postings/lever?skip=1&limit=3)

Fetch all published job postings.

| Query parameter | Description                   |
| --------------- | ----------------------------- |
| skip            | skip N from the start         |
| limit           | only return at most N results |

Each job posting is a JSON object with the following fields:

| name        | Description                   |
| ----------- | ----------------------------- |
| text        | Posting name
| categories  | Object with location, commitment and team
| description | Job description
| lists       | Extra lists of things like requirements from the job posting. This is a list of `{text:NAME, content:"unstyled HTML of list elements"}`
| additional  | Optional closing content for the job posting. May be an empty string.
| id          | Unique Job ID
| applyUrl    | A URL which points to lever's internal application form for the job posting
| tags        | Tags which have been added to the job posting

## Get a specific job posting

> GET /v0/postings/SITE/POSTING-ID

Get the named job posting by id. The fields which are available are the same as the fields exposed by the list API (above).


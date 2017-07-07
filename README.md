# docs
Docs for the migrant-cube project

## Structure of the app

The app will consist of three docker containers put together using `docker-compose`. There will be SQL Server container, a C# REST API serving JSON and a React.js based Single Page Application.

## Proposed API

For the Minimal Viable Product stage, there will be 4 endpoints which are detailed below.

### `GET /api/origins`

This will return the list of all the countries that immigrant applications come from.

```json
[
    "albania",
    "algeria",
    "...",
    "zimbabwe"
]
```

### `GET /api/years`

This will return the list of all years for which immigration data is available.

```json
[
    1991,
    1992,
    1993,
    2004
]
```

### `GET /api/destinations/:country?origin={origin}&year={year}`

This request will take in a country as a destination, a country of origin and a year and return the immigration data for it. The destination country will be part of the request path and the origin and the year will be included as query parameters.

```json
{
    "destination": "canada",
    "origin": "egypt",
    "year": 2004,
    "applied": 400,
    "accepted": 350
}
```

The `origin` query parameter also supports the `all` option which will include all the other countries except for the destination. For example, the request `GET /api/destinations/canada?origin=all&year=2007` will return immigration data from all countries (except Canada) for the year 2007. 

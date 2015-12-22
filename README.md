[![Build Status](https://travis-ci.org/freiheit-com/fdc-test-statistics.svg?branch=master)](https://travis-ci.org/freiheit-com/fdc-test-statistics)

#REST-API:

## Store coverage data:

    curl -kv -X PUT https://<servername>/publish/coverage -d '{"lines": <n>, "covered": <m>, "project": "<project-name>", "subproject": "<subproject-name>", "language": "<language>"}' -H "Content-Type: application/json" -H "auth-token: <publish-auth-token>"

Only the last PUT of the day is remembered by the statistic server.

## Get latest coverage data:

    curl -v https://<servername>/statistics/coverage/latest/<project-name> -H "auth-token: <statistics-auth-token>"

Gives you the most recent coverage data for project `<project-name>`. Looks back at most 30 days.
Aggregates coverage data over all subprojects and languages in `<project-name>`.

## Register a project

    curl -kv -X PUT https://<servername>/meta/project -d '{"project": "<project-name>"", "subproject": "<subproject-name>", "language": "<language>"}' -H "Content-Type: application/json" -H "auth-token: <meta-auth-token>"

Register (project, sub-project, language) with the statistic server. You may not publish data before registering.


#Build

lein ring uberjar (needs https://github.com/weavejester/lein-ring)

NOT lein uberjar (jars produced by this command do not contain the correct start code)

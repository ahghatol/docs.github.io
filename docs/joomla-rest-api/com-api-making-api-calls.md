---
title:       Making calls to API resources
description: Making calls to API resources using REST API framework for Joomla (com_api)
path:        docs/joomla-rest-api
source:      com-api-making-api-calls.md
hero:        Joomla REST API - Making calls to API resources
date:        2017-09-15
categories:
  - Joomla REST API
tags:
  - Joomla
  - REST API
  - com_api
---


## How to call API resources?

To make an API call, We need to set:

 - API URL,
 - authentication headers,
 - output format

### 1. Set API URLs

#### Non-SEF URLs
If you do not have SEF URLs enabled, use  the endpoint URL as

`index.php?option=com_api&app={app}&resource={resource}&format=raw`

Example for users plugin could be:

`index.php?option=com_api&app=users&resource=user&id=619&format=raw`

#### SEF URLs
SEF URL to access any route is of the format

`/api/{plugin}/{resource}`

Example for users plugin could be:

`/api/users/user/619`

!!! info
    To enable SEF URLs for endpoints, make sure you have created a Joomla menu of the type API > API Endpoint. If you create the menu using any other alias than `api` make sure you use the apppropriate slug in the endpoint.

!!! tip
    If your resource expects an `id` parameter in the URL, you can use `/api/{plugin}/{resource}/{id}` as the API url. Other querystring need to be sent as is.

### 2. Set Authentication header
While it is possible for an app to make an entire resource or a specific HTTP method in a resource public, other non-public resources will need API token for authentication.

The token needs to be passed via the Authorization header using the Bearer scheme eg: `Authorization: Bearer <token>`.

!!! info
    - Previous versions also allowed passing the token as a querystring variable with the name `key`. The querystring approach will be deprecated in the future version.

!!! note
    Sometimes Apache does not pass on the Authorization header, in such cases send then token using the X-Authorization header i.e. `X-Authorization: Bearer {token}`

### 3. Set Output Format
The default output format is JSON. However it's also possible to get XML output by setting the `Accept: application/xml` header.

### Example url call
An example curl call may look like this:

``` bash
curl --location --request GET 'http://{{host}}/index.php?option=com_api&app=users&resource=user&id=619&format=raw' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--header 'Authorization: Bearer c8b16517a0a21c446f1ee9980944cd7e'
```

## Overriding Output
If you wish to modify the 'envelope' of the response:

- you can copy the file `components/com_api/libraries/response/jsonresponse.php`
- paste into `templates/{your template}/json/api.php`
- and modify the structure of the output.

!!! info
    A similar override is possible by creating a xml.php as well.

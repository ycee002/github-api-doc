# GitHub API Documentation

## Overview

GitHub's REST API helps you manage your GitHub resources like repositories, users, and organizations. You can automate tasks, integrate with other systems, and extend GitHub's features to fit your development needs.

### Version

**2022-11-28**

### Base URL

```
https://api.github.com
```

### Contact

* **Name:** GitHub API Support
* **Website:** [GitHub Support](https://support.github.com/)
* **Email:** [api-support@github.com](mailto:api-support@github.com)

---

## Endpoints

### GET `/orgs/{org}/repos`

#### Summary

Get Organization Repositories

#### Description

This endpoint retrieves a list of all repositories belonging to a specific GitHub organization.

#### Parameters

| Name | In   | Type   | Required | Description                          |
| ---- | ---- | ------ | -------- | ------------------------------------ |
| org  | path | string | true     | The name of the GitHub organization. |

#### Responses

##### 200 OK

A list of repositories for the specified organization.

**Content Type:** `application/json`

Example Response:

```json
[
  {
    "id": 15929,
    "node_id": "MDEwOlJlcG9zaXRvcnkxNTkyOQ==",
    "name": "albino",
    "full_name": "github/albino",
    "private": false,
    "owner": {
      "login": "github",
      "id": 9919,
      "node_id": "MDEyOk9yZ2FuaXphdGlvbjk5MTk=",
      "type": "Organization",
      "user_view_type": "public",
      "site_admin": false
    }
  }
]
```

##### 404 Not Found

Organization not found.

##### 500 Internal Server Error

Internal server error.

---

### POST `/orgs/{org}/repos`

#### Summary

Create Repository in Organization

#### Description

Use this endpoint to create a brand new repository within a specified organization on GitHub.

#### Security

Authentication required: Bearer Token (JWT)

#### Parameters

| Name | In   | Type   | Required | Description                          |
| ---- | ---- | ------ | -------- | ------------------------------------ |
| org  | path | string | true     | The name of the GitHub organization. |

#### Request Body

**Required:** Yes

**Content Type:** `application/json`

Example Request:

```json
{
  "name": "Ehizzymonie-programmer",
  "description": "API integration project to document Ehizzymonie programmer",
  "homepage": "https://github.com/myfashionhub/Ehizzy-programmer",
  "private": false,
  "has_issues": true,
  "has_projects": true,
  "has_wiki": false
}
```

#### Responses

##### 201 Created

Repository created successfully.

Example Response:

```json
{
  "id": 1011333072,
  "name": "Ehizzymonie-programmer",
  "full_name": "myfashionhub1234/Ehizzymonie-programmer",
  "private": false,
  "owner": {
    "login": "myfashionhub1234",
    "id": 218431065,
    "type": "Organization",
    "user_view_type": "public"
  }
}
```

##### 400 Bad Request

Invalid input data.

##### 401 Unauthorized

Authentication required.

##### 404 Not Found

Organization not found.

##### 500 Internal Server Error

Internal server error.

---

### GET `/repos/{owner}/{repo}`

#### Summary

Get Repository Details

#### Description

This endpoint fetches detailed information about a specific repository on GitHub.

#### Parameters

| Name  | In   | Type   | Required | Description                                                 |
| ----- | ---- | ------ | -------- | ----------------------------------------------------------- |
| owner | path | string | true     | The username or organization name that owns the repository. |
| repo  | path | string | true     | The name of the repository.                                 |

#### Responses

##### 200 OK

Repository details retrieved successfully.

Example Response:

```json
{
  "id": 1010657333,
  "name": "Ycee-tech-writer",
  "full_name": "myfashionhub1234/Ycee-tech-writer",
  "private": false,
  "owner": {
    "login": "myfashionhub1234",
    "id": 218431065,
    "type": "Organization",
    "user_view_type": "public",
    "site_admin": false
  }
}
```

##### 404 Not Found

Repository not found.

##### 500 Internal Server Error

Internal server error.

---

### PATCH `/repos/{owner}/{repo}`

#### Summary

Update Repository

#### Description

Use this endpoint to modify the details of an existing repository on GitHub.

#### Security

Authentication required: Bearer Token (JWT)

#### Parameters

| Name  | In   | Type   | Required | Description                                                 |
| ----- | ---- | ------ | -------- | ----------------------------------------------------------- |
| owner | path | string | true     | The username or organization name that owns the repository. |
| repo  | path | string | true     | The name of the repository.                                 |

#### Request Body

**Required:** Yes

**Content Type:** `application/json`

Example Request:

```json
{
  "name": "Zolando-fashion",
  "description": "This is an updated description for the repository.",
  "private": true
}
```

#### Responses

##### 200 OK

Repository updated successfully.

Example Response:

```json
{
  "id": 1011387773,
  "name": "Zolando-fashion",
  "full_name": "myfashionhub1234/Zolando-fashion",
  "private": false,
  "owner": {
    "login": "myfashionhub1234",
    "id": 218431065,
    "type": "Organization",
    "user_view_type": "public"
  }
}
```

##### 400 Bad Request

Invalid input data.

##### 401 Unauthorized

Authentication required.

##### 404 Not Found

Repository not found.

##### 500 Internal Server Error

Internal server error.

---

### GET `/user`

#### Summary

Get All Users

#### Description

This endpoint returns a comprehensive list of all publicly available users on GitHub.

#### Responses

##### 200 OK

Example Response:

```json
[
  {
    "login": "mojombo",
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "type": "User",
    "user_view_type": "public"
  }
]
```

##### 500 Internal Server Error

Internal server error.

---

### GET `/users/{username}`

#### Summary

Get User Profile

#### Description

Use this endpoint to retrieve the public profile information for any specific GitHub user.

#### Parameters

| Name     | In   | Type   | Required | Description                      |
| -------- | ---- | ------ | -------- | -------------------------------- |
| username | path | string | true     | The username of the GitHub user. |

#### Responses

##### 200 OK

Example Response:

```json
{
  "login": "ycee002",
  "id": 199307583,
  "node_id": "U_kgDOC-ExPw",
  "created_at": "2025-02-14T22:55:02Z",
  "updated_at": "2025-06-10T20:13:54Z"
}
```

##### 404 Not Found

User not found.

##### 500 Internal Server Error

Internal server error.

---

### GET `/rate_limit`

#### Summary

Get API Rate Limit Status

#### Description

This endpoint shows your current API rate limit status, including how many requests you have remaining and when the limit resets.

#### Responses

##### 200 OK

Example Response:

```json
{
  "resources": {
    "core": {
      "limit": 60,
      "remaining": 59,
      "reset": 1751319801,
      "used": 1,
      "resource": "core"
    }
  },
  "rate": {
    "limit": 60,
    "remaining": 59,
    "reset": 1751319801,
    "used": 1,
    "resource": "core"
  }
}
```

##### 500 Internal Server Error

Internal server error.

---

## Components

### Security Schemes

#### BearerAuth

| Type | Scheme | Bearer Format | Description                                             |
| ---- | ------ | ------------- | ------------------------------------------------------- |
| http | bearer | JWT           | Enter your Bearer token in the format `Bearer <token>`. |

### Parameters

| Name     | In   | Type   | Required | Description                                                 | Example          |
| -------- | ---- | ------ | -------- | ----------------------------------------------------------- | ---------------- |
| org      | path | string | true     | The name of the organization on GitHub.                     | github           |
| owner    | path | string | true     | The username or organization name that owns the repository. | myfashionhub1234 |
| repo     | path | string | true     | The name of the repository you want to access.              | Ycee-tech-writer |
| username | path | string | true     | The specific GitHub username to retrieve information for.   | Ycee002          |

### Schemas

(Your schemas table content here)

---

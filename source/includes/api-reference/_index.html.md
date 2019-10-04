<!-- Generator: Widdershins v3.6.6 -->

<hr class="full-line">
<h1 id="asana">API Reference</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

This is the interface for interacting with the [Asana Platform](https://developers.asana.com). Our API reference is generated from our [OpenAPI spec] (https://raw.githubusercontent.com/Asana/developer-docs/master/defs/asana_oas.yaml).

Base URLs:

* <a href="https://app.asana.com/api/1.0">https://app.asana.com/api/1.0</a>

<a href="https://asana.com/terms">Terms of service</a>
Web: <a href="https://asana.com/support">Asana Support</a> 
License: <a href="https://www.apache.org/licenses/LICENSE-2.0">Apache 2.0</a>

<hr class="full-line">
<h1 id="asana-attachments">Attachments</h1>

<pre class="highlight http tab-http">
<code><a href="#get-an-attachment"><span class="get-verb">GET</span> <span class=""nn>/attachments/{attachment_gid}</span></a><br><a href="#get-attachments-for-a-task"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/attachments</span></a><br><a href="#upload-an-attachment"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/attachments</span></a></code>
</pre>

An *attachment* object represents any file attached to a task in Asana, whether it’s an uploaded file or one associated via a third-party service such as Dropbox or Google Drive.

<hr class="half-line">
## Get an attachment

<a id="opIdgetAttachment"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/attachments/{attachment_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /attachments/{attachment_gid}</code>
</p>

Get the full record for a single attachment.

<h3 id="get-an-attachment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|attachment_gid|path|string|true|Globally unique identifier for the attachment.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "attachment",
    "name": "Screenshot.png",
    "created_at": "2012-02-22T02:06:58.147Z",
    "download_url": "https://www.dropbox.com/s/123/Screenshot.png?dl=1",
    "host": "dropbox",
    "parent": null,
    "view_url": "https://www.dropbox.com/s/123/Screenshot.png"
  }
}
```

<h3 id="get-an-attachment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the record for a single attachment.|[Attachment](#schemaattachment)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|402|[Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2)|The request was valid, but the queried object or object mutation specified in the request is above your current premium level.|None|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|424|[Failed Dependency](https://tools.ietf.org/html/rfc2518#section-10.5)|You have exceeded one of the enforced rate limits in the API. See the [documentation on rate limiting](https://developers.asana.com/docs/#rate-limits) for more information.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|
|501|[Not Implemented](https://tools.ietf.org/html/rfc7231#section-6.6.2)|There is an issue between the load balancers and Asana's API.|[Error](#schemaerror)|
|503|[Service Unavailable](https://tools.ietf.org/html/rfc7231#section-6.6.4)|Either the upstream service is unavailable to the API, or he API has been intentionally shut off.|[Error](#schemaerror)|
|504|[Gateway Time-out](https://tools.ietf.org/html/rfc7231#section-6.6.5)|This request took too long to complete.|[Error](#schemaerror)|

<hr class="half-line">
## Get attachments for a task

<a id="opIdgetAttachmentsForTask"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/attachments \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/attachments</code>
</p>

Returns the compact records for all attachments on the task.

<h3 id="get-attachments-for-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "attachment",
      "name": "Screenshot.png"
    }
  ]
}
```

<h3 id="get-attachments-for-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the compact records for all attachments on the task.|[Attachment](#schemaattachment)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Upload an attachment

<a id="opIduploadAttachmentToTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/attachments \
  -H 'Content-Type: multipart/form-data' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/attachments</code>
</p>

Upload an attachment.

This method uploads an attachment to a task and returns the compact
record for the created attachment object. It is not possible to attach
files from third party services such as Dropbox, Box & Google Drive via
the API. You must download the file content first and then upload it as
any other attachment.

The 100MB size limit on attachments in Asana is enforced on this endpoint.

This endpoint expects a multipart/form-data encoded request containing
the full contents of the file to be uploaded.

Requests made should follow the HTTP/1.1 specification that line
terminators are of the form `CRLF` or `\r\n` outlined
[here](http://www.w3.org/Protocols/HTTP/1.1/draft-ietf-http-v11-spec-01#Basic-Rules)
in order for the server to reliably and properly handle the request.

> Body parameter

```yaml
file: string

```

<h3 id="upload-an-attachment-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The file you want to upload.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

#### Detailed descriptions

**body**: The file you want to upload.

*Note when using curl:*

Be sure to add an `‘@’` before the file path, and use the `—form`
option instead of the `-d` option.

When uploading PDFs with curl, force the content-type to be pdf by
appending the content type to the file path: `—form
“file=@file.pdf;type=application/pdf”`.

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "attachment",
    "name": "Screenshot.png",
    "created_at": "2012-02-22T02:06:58.147Z",
    "download_url": "https://www.dropbox.com/s/123/Screenshot.png?dl=1",
    "host": "dropbox",
    "parent": null,
    "view_url": "https://www.dropbox.com/s/123/Screenshot.png"
  }
}
```

<h3 id="upload-an-attachment-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully uploaded the attachment to the task.|[Attachment](#schemaattachment)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-batch-api">Batch API</h1>

<pre class="highlight http tab-http">
<code><a href="#submit-parallel-requests"><span class="post-verb">POST</span> <span class=""nn>/batch</span></a></code>
</pre>

There are many cases where you want to accomplish a variety of work in the Asana API but want to minimize the number of HTTP requests you make. For example:

* Modern browsers limit the number of requests that a single web page can
  make at once.
* Mobile apps will use more battery life to keep the cellular radio on
  when making a series of requests.
* There is an overhead cost to developing software that can make multiple
  requests in parallel.
* Some cloud platforms handle parallelism poorly, or disallow it
  entirely.

To make development easier in these use cases, Asana provides a **batch API** that enables developers to perform multiple “actions” by making only a single HTTP request.

#### Making a Batch Request

To make a batch request, send a `POST` request to `/batch`. Like other `POST` endpoints, the body should contain a `data` envelope. Inside this envelope should be a single `actions` field, containing a list of “action” objects.  Each action represents a standard request to an existing endpoint in the Asana API.

**The maximum number of actions allowed in a single batch request is 10**. Making a batch request with no actions in it will result in a `400 Bad Request`.

When the batch API receives the list of actions to execute, it will dispatch those actions to the already-implemented endpoints specified by the `relative_path` and `method` for each action. This happens in parallel, so all actions in the request will be processed simultaneously. There is no guarantee of the execution order for these actions, nor is there a way to use the output of one action as the input of another action (such as creating a task and then commenting on it).

The response to the batch request will contain (within the `data` envelope) a list of result objects, one for each action. The results are guaranteed to be in the same order as the actions in the request, e.g., the first result in the response corresponds to the first action in the request.

The batch API will always attempt to return a `200 Success` response with individual result objects for each individual action in the request. Only in certain cases (such as missing authorization or malformed JSON in the body) will the entire request fail with another status code. Even if every individual action in the request fails, the batch API will still return a `200 Success` response, and each result object in the response will contain the errors encountered with each action.

#### Rate Limiting

The batch API fully respects all of our rate limiting. This means that a batch request counts against *both* the standard rate limiter and the concurrent request limiter as though you had made a separate HTTP request for every individual action. For example, a batch request with five actions counts as five separate requests in the standard rate limiter, and counts as five concurrent requests in the concurrent request limiter. The batch request itself incurs no cost.

If any of the actions in a batch request would exceed any of the enforced limits, the *entire* request will fail with a `429 Too Many Requests` error. This is to prevent the unpredictability of which actions might succeed if not all of them could succeed.

#### Restrictions

Not every endpoint can be accessed through the batch API. Specifically, the following actions cannot be taken and will result in a `400 Bad Request` for that action:

* Uploading attachments
* Creating, getting, or deleting organization exports
* Any SCIM operations
* Nested calls to the batch API

<hr class="half-line">
## Submit parallel requests

<a id="opIdbatchRequest"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/batch \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /batch</code>
</p>

Make multiple requests in parallel to Asana's API.

> Body parameter

```json
{
  "data": {
    "actions": [
      {
        "relative_path": "/tasks/123",
        "method": "get",
        "data": {
          ...
        },
        "options": {
          ...
        }
      }
    ]
  }
}
```

<h3 id="submit-parallel-requests-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The requests to batch together via the Batch API.|
|» data|body|object|false|none|
|»» actions|body|[[BatchRequest](#schemabatchrequest)]|false|[A request object for use in a batch request.]|
|»»» relative_path|body|string|true|The path of the desired endpoint relative to the API’s base URL. Query parameters are not accepted here; put them in `data` instead.|
|»»» method|body|string|true|The HTTP method you wish to emulate for the action.|
|»»» data|body|object|false|For `GET` requests, this should be a map of query parameters you would have normally passed in the URL. Options and pagination are not accepted here; put them in `options` instead. For `POST`, `PATCH`, and `PUT` methods, this should be the content you would have normally put in the data field of the body.|
|»»» options|body|object|false|Pagination (`limit` and `offset`) and output options (`fields` or `expand`) for the action. “Pretty” JSON output is not an available option on individual actions; if you want pretty output, specify that option on the parent request.|
|»»»» limit|body|integer|false|Pagination limit for the request.|
|»»»» offset|body|integer|false|Pagination offset for the request.|
|»»»» fields|body|[string]|false|The fields to retrieve in the request.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Enumerated Values

|Parameter|Value|
|---|---|
| method|get|
| method|post|
| method|put|
| method|delete|
| method|patch|
| method|head|

> 200 Response

```json
{
  "data": [
    {
      "status_code": 200,
      "headers": {
        "location": "/tasks/1234"
      },
      "body": {
        "data": {
          ...
        }
      }
    }
  ]
}
```

<h3 id="submit-parallel-requests-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully completed the requested batch API operations.|[BatchResult](#schemabatchresult)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-custom-fields">Custom Fields</h1>

<pre class="highlight http tab-http">
<code><a href="#create-a-custom-field"><span class="post-verb">POST</span> <span class=""nn>/custom_fields</span></a><br><a href="#get-a-custom-field"><span class="get-verb">GET</span> <span class=""nn>/custom_fields/{custom_field_gid}</span></a><br><a href="#update-a-custom-field"><span class="put-verb">PUT</span> <span class=""nn>/custom_fields/{custom_field_gid}</span></a><br><a href="#delete-a-custom-field"><span class="delete-verb">DELETE</span> <span class=""nn>/custom_fields/{custom_field_gid}</span></a><br><a href="#get-a-workspace-39-s-custom-fields"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/custom_fields</span></a><br><a href="#create-an-enum-option"><span class="post-verb">POST</span> <span class=""nn>/custom_fields/{custom_field_gid}/enum_options</span></a><br><a href="#reorder-a-custom-field-39-s-enum"><span class="post-verb">POST</span> <span class=""nn>/custom_fields/{custom_field_gid}/enum_options/insert</span></a><br><a href="#update-an-enum-option"><span class="put-verb">PUT</span> <span class=""nn>/enum_options/{enum_option_gid}</span></a></code>
</pre>

In the Asana application, Tasks can hold user-specified Custom Fields which provide extra information; for example, a priority value or a number representing the time required to complete a Task. This lets a user define the type of information that each Task within a Project can contain in addition to the built-in fields that Asana provides.

**Note:** Custom Fields are a premium feature. Integrations which work with Custom Fields need to handle an assortment of use cases for free and premium users in context of free and premium organizations. For a detailed examination of to what data users will have access in different circumstances, read the section below on [access control](#access-control).

The characteristics of Custom Fields are:

* There is metadata that defines the Custom Field. This metadata is shared across an entire organization or workspace. * Projects can have Custom Fields associated with them individually. This is conceptually akin to adding columns in a database or a spreadsheet: every Task (row) in the Project (table) can contain information for that field, including "blank" values, i.e. `null` data. * Tasks have Custom Field _values_ assigned to them.

A brief example: let's imagine that an organization has defined a Custom Field for "Priority". This field is of `enum` type and can have user-defined values of `Low`, `Medium`, or `High`. This is the field metadata, and it is visible within, and shared across, the entire organization.

A Project is then created in the organization, called "Bugs", and the "Priority" Custom Field is associated with that Project. This will allow all Tasks within the "Bugs" Project to have an associated "Priority".

A new Task is created within "Bugs". This Task, then, has a field named "Priority" which can take on the Custom Field value of one of `[null]`, `Low`, `Medium`, and `High`.

These Custom Fields are accessible via the API through a number of endpoints at the top level (e.g. `/custom_fields` and `/custom_field_settings`) and through calls on Workspaces, Projects, and Tasks resources. The API also provides a way to fetch both the metadata and data which define each particular Custom Field, so that a client application may render proper UI to display or edit the values.

Custom Field aware integrations need to be aware of the basic types that Custom Fields can adopt. These types are:

* `text` - an arbitrary, relatively short string of text * `number` - a number with a defined level of precision * `enum` - a selection from a defined list of options

Text fields are currently limited to 1024 characters. On Tasks, their Custom Field value will have a `text_value` property to represent this field.

Number fields can have an arbitrary `precision` associated with them; for example, a precision of `2` would round its value to the second (hundredths) place, i.e. 1.2345 would round to 1.23. On Tasks, the Custom Field value will have a `number_value` property to represent this field.

Enum fields represent a selection from a list of options. On the metadata, they will contain all of the options in an array. Each option has 4 properties:

* `id` - the id of this enum option. Note that this is the id of the _option_ - the Custom Field itself has a separate `id`. * `name` - the name of the option, e.g. "Choice #1" * `enabled` - whether this field is enabled. Disabled fields are not available to choose from when disabled, and are visually hidden in the Asana application, but they remain in the metadata for Custom Field values which were set to the option before the option was disabled. * `color` - a color associated with this choice.

On the Task's Custom Field value, the enum will have an `enum_value` property which will be the same as one of the choices from the list defined in the Custom Field metadata.

<hr class="half-line">
## Create a custom field

<a id="opIdcreateCustomField"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/custom_fields \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /custom_fields</code>
</p>

Creates a new custom field in a workspace. Every custom field is required
to be created in a specific workspace, and this workspace cannot be
changed once set.

A custom field’s name must be unique within a workspace and not conflict
with names of existing task properties such as ‘Due Date’ or ‘Assignee’.
A custom field’s type must be one of ‘text’, ‘enum’, or ‘number’.

Returns the full record of the newly created custom field.

> Body parameter

```json
{
  "data": {
    "name": "Bug Task",
    "type": "text",
    "enum_options": [
      {
        ...
      }
    ],
    "enum_value": null,
    "enabled": true,
    "text_value": "Some Value",
    "description": "Development team priority",
    "precision": 2,
    "has_notifications_enabled": true,
    "workspace": "1331"
  }
}
```

<h3 id="create-a-custom-field-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|The custom field object to create.|
|» data|body|object|false|Custom Fields store the metadata that is used in order to add user-specified information to tasks in Asana. Be sure to reference the [Custom Fields](#asana-custom-fields) developer documentation for more information about how custom fields relate to various resources in Asana.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|The name of the object.|
|»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»» type|body|string|false|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|»» enum_options|body|[object]|false|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|The name of the enum option.|
|»»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|»» enum_value|body|any|false|none|
|»» enabled|body|boolean|false|*Conditional*. Determines if the custom field is enabled or not.|
|»» text_value|body|string|false|*Conditional*. This string is the value of a text custom field.|
|»» description|body|string|false|[Opt In](#input-output-options). The description of the custom field.|
|»» precision|body|integer|false|Only relevant for custom fields of type ‘Number’. This field dictates the number of places after the decimal to round to, i.e. 0 is integer values, 1 rounds to the nearest tenth, and so on. Must be between 0 and 6, inclusive.|
|»» is_global_to_workspace|body|boolean|false|This flag describes whether this custom field is available to every container in the workspace. Before project-specific custom fields, this field was always true.|
|»» has_notifications_enabled|body|boolean|false|This flag describes whether a follower of a task with this field should receive inbox notifications from changes to this field.|
|»» workspace|body|string|true|The workspace to create a custom field in.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

#### Enumerated Values

|Parameter|Value|
|---|---|
| type|text|
| type|enum|
| type|number|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "custom_field",
    "name": "Bug Task",
    "resource_subtype": "milestone",
    "type": "text",
    "enum_options": [
      {
        ...
      }
    ],
    "enum_value": null,
    "enabled": true,
    "text_value": "Some Value",
    "description": "Development team priority",
    "precision": 2,
    "is_global_to_workspace": true,
    "has_notifications_enabled": true
  }
}
```

<h3 id="create-a-custom-field-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Custom field successfully created.|[CustomField](#schemacustomfield)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a custom field

<a id="opIdgetCustomField"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/custom_fields/{custom_field_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /custom_fields/{custom_field_gid}</code>
</p>

Get the complete definition of a custom field’s metadata.

Since custom fields can be defined for one of a number of types, and
these types have different data and behaviors, there are fields that are
relevant to a particular type. For instance, as noted above, enum_options
is only relevant for the enum type and defines the set of choices that
the enum could represent. The examples below show some of these
type-specific custom field definitions.

<h3 id="get-a-custom-field-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|custom_field_gid|path|string|true|Globally unique identifier for the custom field.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "custom_field",
    "name": "Bug Task",
    "resource_subtype": "milestone",
    "type": "text",
    "enum_options": [
      {
        ...
      }
    ],
    "enum_value": null,
    "enabled": true,
    "text_value": "Some Value",
    "description": "Development team priority",
    "precision": 2,
    "is_global_to_workspace": true,
    "has_notifications_enabled": true
  }
}
```

<h3 id="get-a-custom-field-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the complete definition of a custom field’s metadata.|[CustomField](#schemacustomfield)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a custom field

<a id="opIdupdateCustomField"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/custom_fields/{custom_field_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /custom_fields/{custom_field_gid}</code>
</p>

A specific, existing custom field can be updated by making a PUT request on the URL for that custom field. Only the fields provided in the `data` block will be updated; any unspecified fields will remain unchanged
When using this method, it is best to specify only those fields you wish to change, or else you may overwrite changes made by another user since you last retrieved the custom field.
A custom field’s `type` cannot be updated.
An enum custom field’s `enum_options` cannot be updated with this endpoint. Instead see “Work With Enum Options” for information on how to update `enum_options`.
Locked custom fields can only be updated by the user who locked the field.
Returns the complete updated custom field record.

> Body parameter

```json
{
  "data": {
    "name": "Bug Task",
    "type": "text",
    "enum_options": [
      {
        ...
      }
    ],
    "enum_value": null,
    "enabled": true,
    "text_value": "Some Value",
    "description": "Development team priority",
    "precision": 2,
    "has_notifications_enabled": true
  }
}
```

<h3 id="update-a-custom-field-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[CustomFieldObject](#schemacustomfieldobject)|false|The custom field object with all updated properties.|
|custom_field_gid|path|string|true|Globally unique identifier for the custom field.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "custom_field",
    "name": "Bug Task",
    "resource_subtype": "milestone",
    "type": "text",
    "enum_options": [
      {
        ...
      }
    ],
    "enum_value": null,
    "enabled": true,
    "text_value": "Some Value",
    "description": "Development team priority",
    "precision": 2,
    "is_global_to_workspace": true,
    "has_notifications_enabled": true
  }
}
```

<h3 id="update-a-custom-field-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|The custom field was successfully updated.|[CustomField](#schemacustomfield)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a custom field

<a id="opIddeleteCustomField"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/custom_fields/{custom_field_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /custom_fields/{custom_field_gid}</code>
</p>

A specific, existing custom field can be deleted by making a DELETE request on the URL for that custom field.
Locked custom fields can only be deleted by the user who locked the field.
Returns an empty data record.

<h3 id="delete-a-custom-field-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|custom_field_gid|path|string|true|Globally unique identifier for the custom field.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-custom-field-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|The custom field was successfully deleted.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a workspace's custom fields

<a id="opIdgetCustomFieldsInWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/custom_fields \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/custom_fields</code>
</p>

Returns a list of the compact representation of all of the custom fields in a workspace.

<h3 id="get-a-workspace's-custom-fields-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "custom_field",
      "name": "Bug Task",
      "resource_subtype": "milestone",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value"
    }
  ]
}
```

<h3 id="get-a-workspace's-custom-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved all custom fields for the given workspace.|[CustomField](#schemacustomfield)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create an enum option

<a id="opIdaddEnumOption"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/custom_fields/{custom_field_gid}/enum_options \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /custom_fields/{custom_field_gid}/enum_options</code>
</p>

Creates an enum option and adds it to this custom field’s list of enum options. A custom field can have at most 50 enum options (including disabled options). By default new enum options are inserted at the end of a custom field’s list.
Locked custom fields can only have enum options added by the user who locked the field.
Returns the full record of the newly created enum option.

> Body parameter

```json
{
  "data": {
    "name": "Low",
    "enabled": true,
    "color": "blue",
    "insert_before": "12345",
    "insert_after": "12345"
  }
}
```

<h3 id="create-an-enum-option-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|The enum option object to create.|
|» data|body|object|false|Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|The name of the enum option.|
|»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|»» insert_before|body|string|false|An existing enum option within this custom field before which the new enum option should be inserted. Cannot be provided together with after_enum_option.|
|»» insert_after|body|string|false|An existing enum option within this custom field after which the new enum option should be inserted. Cannot be provided together with before_enum_option.|
|custom_field_gid|path|string|true|Globally unique identifier for the custom field.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "enum_option",
    "name": "Low",
    "enabled": true,
    "color": "blue"
  }
}
```

<h3 id="create-an-enum-option-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Custom field enum option successfully created.|[EnumOption](#schemaenumoption)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Reorder a custom field's enum

<a id="opIdreorderEnumOption"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/custom_fields/{custom_field_gid}/enum_options/insert \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /custom_fields/{custom_field_gid}/enum_options/insert</code>
</p>

Moves a particular enum option to be either before or after another specified enum option in the custom field.
Locked custom fields can only be reordered by the user who locked the field.

> Body parameter

```json
{
  "data": {
    "name": "Low",
    "enabled": true,
    "color": "blue",
    "enum_option": "97285",
    "before_enum_option": "12345",
    "after_enum_option": "12345"
  }
}
```

<h3 id="reorder-a-custom-field's-enum-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|The enum option object to create.|
|» data|body|object|false|Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|The name of the enum option.|
|»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|»» enum_option|body|string|true|The gid of the enum option to relocate.|
|»» before_enum_option|body|string|false|An existing enum option within this custom field before which the new enum option should be inserted. Cannot be provided together with after_enum_option.|
|»» after_enum_option|body|string|false|An existing enum option within this custom field after which the new enum option should be inserted. Cannot be provided together with before_enum_option.|
|custom_field_gid|path|string|true|Globally unique identifier for the custom field.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "enum_option",
    "name": "Low",
    "enabled": true,
    "color": "blue"
  }
}
```

<h3 id="reorder-a-custom-field's-enum-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Custom field enum option successfully reordered.|[EnumOption](#schemaenumoption)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update an enum option

<a id="opIdupdateEnumOption"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/enum_options/{enum_option_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /enum_options/{enum_option_gid}</code>
</p>

Updates an existing enum option. Enum custom fields require at least one enabled enum option.
Locked custom fields can only be updated by the user who locked the field.
Returns the full record of the updated enum option.

> Body parameter

```json
{
  "data": {
    "name": "Low",
    "enabled": true,
    "color": "blue"
  }
}
```

<h3 id="update-an-enum-option-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|The enum option object to update|
|» data|body|[EnumOption](#schemaenumoption)|false|Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|The name of the enum option.|
|»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|enum_option_gid|path|string|false|Globally unique identifier for the enum option.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "enum_option",
    "name": "Low",
    "enabled": true,
    "color": "blue"
  }
}
```

<h3 id="update-an-enum-option-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated the specified custom field enum.|[EnumOption](#schemaenumoption)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-custom-field-settings">Custom Field Settings</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-project-39-s-custom-fields"><span class="get-verb">GET</span> <span class=""nn>/projects/{project_gid}/custom_field_settings</span></a><br><a href="#get-a-portfolio-39-s-custom-fields"><span class="get-verb">GET</span> <span class=""nn>/portfolios/{portfolio_gid}/custom_field_settings</span></a></code>
</pre>

Custom fields are attached to a particular project with the Custom Field Settings resource. This resource both represents the many-to-many join of the Custom Field and Project as well as stores information that is relevant to that particular pairing; for instance, the `is_important` property determines some possible application-specific handling of that custom field.

<hr class="half-line">
## Get a project's custom fields

<a id="opIdgetCustomFieldSettingsForProject"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects/{project_gid}/custom_field_settings \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects/{project_gid}/custom_field_settings</code>
</p>

Returns a list of all of the custom fields settings on a project, in compact form. Note that, as in all queries to collections which return compact representation, `opt_fields` can be used to include more data than is returned in the compact representation. See the [getting started guide on input/output options](https://developers.asana.com/docs/#input-output-options) for more information.

<h3 id="get-a-project's-custom-fields-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "custom_field_setting",
      "project": null,
      "is_important": false,
      "parent": null,
      "custom_field": null
    }
  ]
}
```

<h3 id="get-a-project's-custom-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved custom field settings objects for a project.|[CustomFieldSetting](#schemacustomfieldsetting)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a portfolio's custom fields

<a id="opIdgetCustomFieldSettingsForPortfolio"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/custom_field_settings \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolios/{portfolio_gid}/custom_field_settings</code>
</p>

Returns a list of all of the custom fields settings on a portfolio, in compact form.

<h3 id="get-a-portfolio's-custom-fields-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "custom_field_setting",
      "project": null,
      "is_important": false,
      "parent": null,
      "custom_field": null
    }
  ]
}
```

<h3 id="get-a-portfolio's-custom-fields-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved custom field settings objects for a portfolio.|[CustomFieldSetting](#schemacustomfieldsetting)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-events">Events</h1>

<pre class="highlight http tab-http">
<code><a href="#get-events-on-a-resource"><span class="get-verb">GET</span> <span class=""nn>/events</span></a></code>
</pre>

An *event* is an object representing a change to a resource that was observed by an event subscription.

In general, requesting events on a resource is faster and subject to higher rate limits than requesting the resource itself. Additionally, change events bubble up - listening to events on a project would include when stories are added to tasks in the project, even on subtasks.

Establish an initial sync token by making a request with no sync token. The response will be a `412` error - the same as if the sync token had expired.

Subsequent requests should always provide the sync token from the immediately preceding call.

Sync tokens may not be valid if you attempt to go ‘backward’ in the history by requesting previous tokens, though re-requesting the current sync token is generally safe, and will always return the same results.

When you receive a `412 Precondition Failed` error, it means that the sync token is either invalid or expired. If you are attempting to keep a set of data in sync, this signals you may need to re-crawl the data.

Sync tokens always expire after 24 hours, but may expire sooner, depending on load on the service.

<hr class="half-line">
## Get events on a resource

<a id="opIdgetEvents"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/events?resource=12345 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /events</code>
</p>

Returns the full record for all events that have occurred since the sync
token was created.

A GET request to the endpoint /[path_to_resource]/events can be made in
lieu of including the resource ID in the data for the request.

<h3 id="get-events-on-a-resource-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|resource|query|string|true|A resource ID to subscribe to. The resource can be a task or project.|
|sync|query|string|false|A sync token received from the last request, or none on first sync. Events will be returned from the point in time that the sync token was generated.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Detailed descriptions

**sync**: A sync token received from the last request, or none on first sync. Events will be returned from the point in time that the sync token was generated.
*Note: On your first request, omit the sync token. The response will be the same as for an expired sync token, and will include a new valid sync token.If the sync token is too old (which may happen from time to time) the API will return a `412 Precondition Failed` error, and include a fresh sync token in the response.*

> 200 Response

```json
{
  "data": [
    {
      "user": {
        ...
      },
      "resource": {
        ...
      },
      "type": "task",
      "action": "changed",
      "parent": {
        ...
      },
      "created_at": "2012-02-22T02:06:58.147Z"
    }
  ],
  "sync": "de4774f6915eae04714ca93bb2f5ee81"
}
```

<h3 id="get-events-on-a-resource-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved events.|[Event](#schemaevent)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-jobs">Jobs</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-job-by-id"><span class="get-verb">GET</span> <span class=""nn>/jobs/{job_gid}</span></a></code>
</pre>

Jobs represent processes that handle asynchronous work.
Jobs are created when an endpoint requests an action that will be handled asynchronously. Such as project or task duplication.
Only the creator of the duplication process can access the duplication status of the new object.

<hr class="half-line">
## Get a job by id

<a id="opIdgetJob"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/jobs/{job_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /jobs/{job_gid}</code>
</p>

Returns the full record for a job.

<h3 id="get-a-job-by-id-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|job_gid|path|string|true|Globally unique identifier for the job.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "resource_subtype": "milestone",
    "status": "in_progress",
    "new_project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "new_task": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="get-a-job-by-id-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved Job.|[Job](#schemajob)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-organization-exports">Organization Exports</h1>

<pre class="highlight http tab-http">
<code><a href="#create-an-organization-export-request"><span class="post-verb">POST</span> <span class=""nn>/organization_exports</span></a><br><a href="#get-details-on-an-org-export-request"><span class="get-verb">GET</span> <span class=""nn>/organization_exports/{organization_export_gid}</span></a></code>
</pre>

An *organization_export* object represents a request to export the complete data of an Organization in JSON format.

To export an Organization using this API:

* Create an `organization_export`
  [request](#create-an-organization-export-request)
  and store the id that is returned.
* Request the `organization_export` every few minutes, until the
  `state` field contains ‘finished’.
* Download the file located at the URL in the `download_url` field. * Exports can take a long time, from several minutes to a few hours
  for large Organizations.

*Note: These endpoints are only available to [Service Accounts](https://asana.com/guide/help/premium/service-accounts) of an [Enterprise](https://asana.com/enterprise) Organization.*

<hr class="half-line">
## Create an organization export request

<a id="opIdcreateOrganizationExport"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/organization_exports \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /organization_exports</code>
</p>

This method creates a request to export an Organization. Asana will complete the export at some point after you create the request.

> Body parameter

```json
{
  "data": {
    "organization": "1331"
  }
}
```

<h3 id="create-an-organization-export-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The organization to export.|
|» data|body|object|false|none|
|»» organization|body|string|false|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "created_at": "2012-02-22T02:06:58.147Z",
    "download_url": "https://asana-export.s3.amazonaws.com/export-4632784536274-20170127-43246.json.gz?AWSAccessKeyId=xxxxxxxx",
    "state": "started",
    "organization": {
      "gid": "14916",
      "name": "My Workspace"
    }
  }
}
```

<h3 id="create-an-organization-export-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created organization export request.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<h3 id="create-an-organization-export-request-responseschema">Response Schema</h3>

Status Code **201**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
| data|[OrganizationExport](#schemaorganizationexport)|false|none|An *organization_export* object represents a request to export the complete data of an Organization in JSON format.|
| gid|string|false|read-only|Globally unique identifier of the object, as a string.|
| resource_type|string|false|read-only|The base type of this resource.|
| created_at|string(date-time)|false|read-only|The time at which this resource was created.|
| download_url|string(uri)¦null|false|read-only|Download this URL to retreive the full export of the organization<br>in JSON format. It will be compressed in a gzip (.gz) container.<br><br>*Note: May be null if the export is still in progress or<br>failed.  If present, this URL may only be valid for 1 hour from<br>the time of retrieval. You should avoid persisting this URL<br>somewhere and rather refresh on demand to ensure you do not keep<br>stale URLs.*|
| state|string|false|read-only|The current state of the export.|
| organization|object|false|none|*Create-only*: The Organization that is being exported. This can only be specified at create time.|
| gid|string|false|none|none|
| name|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|state|pending|
|state|started|
|state|finished|
|state|error|

<hr class="half-line">
## Get details on an org export request

<a id="opIdgetOrganizationExport"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/organization_exports/{organization_export_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /organization_exports/{organization_export_gid}</code>
</p>

Returns details of a previously-requested Organization export.

<h3 id="get-details-on-an-org-export-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|organization_export_gid|path|string|true|Globally unique identifier for the organization export.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "created_at": "2012-02-22T02:06:58.147Z",
    "download_url": "https://asana-export.s3.amazonaws.com/export-4632784536274-20170127-43246.json.gz?AWSAccessKeyId=xxxxxxxx",
    "state": "started",
    "organization": {
      "gid": "14916",
      "name": "My Workspace"
    }
  }
}
```

<h3 id="get-details-on-an-org-export-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved organization export object.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<h3 id="get-details-on-an-org-export-request-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
| data|[OrganizationExport](#schemaorganizationexport)|false|none|An *organization_export* object represents a request to export the complete data of an Organization in JSON format.|
| gid|string|false|read-only|Globally unique identifier of the object, as a string.|
| resource_type|string|false|read-only|The base type of this resource.|
| created_at|string(date-time)|false|read-only|The time at which this resource was created.|
| download_url|string(uri)¦null|false|read-only|Download this URL to retreive the full export of the organization<br>in JSON format. It will be compressed in a gzip (.gz) container.<br><br>*Note: May be null if the export is still in progress or<br>failed.  If present, this URL may only be valid for 1 hour from<br>the time of retrieval. You should avoid persisting this URL<br>somewhere and rather refresh on demand to ensure you do not keep<br>stale URLs.*|
| state|string|false|read-only|The current state of the export.|
| organization|object|false|none|*Create-only*: The Organization that is being exported. This can only be specified at create time.|
| gid|string|false|none|none|
| name|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|state|pending|
|state|started|
|state|finished|
|state|error|

<hr class="full-line">
<h1 id="asana-portfolios">Portfolios</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-portfolios"><span class="get-verb">GET</span> <span class=""nn>/portfolios</span></a><br><a href="#create-a-portfolio"><span class="post-verb">POST</span> <span class=""nn>/portfolios</span></a><br><a href="#get-a-portfolio"><span class="get-verb">GET</span> <span class=""nn>/portfolios/{portfolio_gid}</span></a><br><a href="#update-a-portfolio"><span class="put-verb">PUT</span> <span class=""nn>/portfolios/{portfolio_gid}</span></a><br><a href="#delete-a-portfolio"><span class="delete-verb">DELETE</span> <span class=""nn>/portfolios/{portfolio_gid}</span></a><br><a href="#get-portfolio-items"><span class="get-verb">GET</span> <span class=""nn>/portfolios/{portfolio_gid}/items</span></a><br><a href="#add-a-portfolio-item"><span class="post-verb">POST</span> <span class=""nn>/portfolios/{portfolio_gid}/addItem</span></a><br><a href="#remove-a-portfolio-item"><span class="post-verb">POST</span> <span class=""nn>/portfolios/{portfolio_gid}/removeItem</span></a><br><a href="#add-users-to-a-portfolio"><span class="post-verb">POST</span> <span class=""nn>/portfolios/{portfolio_gid}/addMembers</span></a><br><a href="#remove-users-from-a-portfolio"><span class="post-verb">POST</span> <span class=""nn>/portfolios/{portfolio_gid}/removeMembers</span></a><br><a href="#add-a-custom-field-to-a-portfolio"><span class="post-verb">POST</span> <span class=""nn>/portfolios/{portfolio_gid}/addCustomFieldSetting</span></a><br><a href="#remove-a-custom-field-from-a-portfolio"><span class="post-verb">POST</span> <span class=""nn>/portfolios/{portfolio_gid}/removeCustomFieldSetting</span></a></code>
</pre>

A 'portfolio' gives a high-level overview of the status of multiple initiatives in Asana. Portfolios provide a dashboard overview of the state of multiple projects, including a progress report and the most recent [project status](#asana-project-statuses) update.
Portfolios have some restrictions on size. Each portfolio has a max of 250 items and, like projects, a max of 20 custom fields.

<hr class="half-line">
## Get multiple portfolios

<a id="opIdgetPortfolios"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolios \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolios</code>
</p>

Returns a list of the portfolios in compact representation that are owned by the current API user.

<h3 id="get-multiple-portfolios-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|workspace|query|string|false|The workspace or organization to filter portfolios on.|
|owner|query|string|false|The user who owns the portfolio. Currently, API users can only get a list of portfolios that they themselves own.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "portfolio",
      "name": "Bug Task"
    }
  ]
}
```

<h3 id="get-multiple-portfolios-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved portfolios.|[Portfolio](#schemaportfolio)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a portfolio

<a id="opIdcreatePortfolio"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios</code>
</p>

Creates a new portfolio in the given workspace with the supplied name.

Note that portfolios created in the Asana UI may have some state
(like the “Priority” custom field) which is automatically added
to the portfolio when it is created. Portfolios created via our
API will *not* be created with the same initial state to allow
integrations to create their own starting state on a portfolio.

> Body parameter

```json
{
  "data": {
    "name": "Bug Task",
    "color": "light-green",
    "owner": null,
    "workspace": null,
    "members": null
  }
}
```

<h3 id="create-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[PortfolioObject](#schemaportfolioobject)|true|The portfolio to create.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "portfolio",
      "name": "Bug Task"
    }
  ]
}
```

<h3 id="create-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully retrieved portfolios.|[Portfolio](#schemaportfolio)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a portfolio

<a id="opIdgetPortfolio"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolios/{portfolio_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolios/{portfolio_gid}</code>
</p>

Returns the complete portfolio record for a single portfolio.

<h3 id="get-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "portfolio",
    "name": "Bug Task",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "color": "light-green",
    "custom_field_settings": [
      {
        ...
      }
    ],
    "owner": null,
    "workspace": null,
    "members": null
  }
}
```

<h3 id="get-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested portfolio.|[Portfolio](#schemaportfolio)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a portfolio

<a id="opIdupdateportfolio"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/portfolios/{portfolio_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /portfolios/{portfolio_gid}</code>
</p>

An existing portfolio can be updated by making a PUT request on the URL for
that portfolio. Only the fields provided in the `data` block will be updated;
any unspecified fields will remain unchanged.

Returns the complete updated portfolio record.

> Body parameter

```json
{
  "data": {
    "name": "Bug Task",
    "color": "light-green",
    "owner": null,
    "workspace": null,
    "members": null
  }
}
```

<h3 id="update-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[PortfolioObject](#schemaportfolioobject)|true|The updated fields for the portfolio.|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "portfolio",
    "name": "Bug Task",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "color": "light-green",
    "custom_field_settings": [
      {
        ...
      }
    ],
    "owner": null,
    "workspace": null,
    "members": null
  }
}
```

<h3 id="update-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated the portfolio.|[Portfolio](#schemaportfolio)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a portfolio

<a id="opIddeletePortfolio"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/portfolios/{portfolio_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /portfolios/{portfolio_gid}</code>
</p>

An existing portfolio can be deleted by making a DELETE request on
the URL for that portfolio.

Returns an empty data record.

<h3 id="delete-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully deleted the specified portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get portfolio items

<a id="opIdgetPortfolioItems"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/items \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolios/{portfolio_gid}/items</code>
</p>

Get a list of the items in compact form in a portfolio.

<h3 id="get-portfolio-items-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy",
      "created_at": "2012-02-22T02:06:58.147Z",
      "archived": false,
      "color": "light-green",
      "current_status": {
        ...
      },
      "custom_fields": [
        ...
      ],
      "custom_field_settings": [
        ...
      ],
      "default_view": "calendar",
      "due_date": "2012-03-26",
      "due_on": "2012-03-26",
      "followers": [
        ...
      ],
      "html_notes": "These are things we need to purchase.",
      "is_template": false,
      "layout": "list",
      "members": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "These are things we need to purchase.",
      "owner": null,
      "public": false,
      "section_migration_status": "not_migrated",
      "start_on": "2012-03-26",
      "team": null,
      "workspace": null
    }
  ]
}
```

<h3 id="get-portfolio-items-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested portfolio's items.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a portfolio item

<a id="opIdaddPortfolioItem"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/addItem?item=1331&insert_before=1331&insert_after=1331 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios/{portfolio_gid}/addItem</code>
</p>

Add an item to a portfolio.
Returns an empty data block.

<h3 id="add-a-portfolio-item-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|item|query|string|true|The item to add to the portfolio.|
|insert_before|query|string|true|An id of an item in this portfolio. The new item will be added before the one specified here. `insert_before` and `insert_after` parameters cannot both be specified.|
|insert_after|query|string|true|An id of an item in this portfolio. The new item will be added after the one specified here. `insert_before` and `insert_after` parameters cannot both be specified.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-a-portfolio-item-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the item to the portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a portfolio item

<a id="opIdremovePortfolioItem"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/removeItem?item=1331 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios/{portfolio_gid}/removeItem</code>
</p>

Remove an item from a portfolio.
Returns an empty data block.

<h3 id="remove-a-portfolio-item-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|item|query|string|true|The item to remove from the portfolio.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-a-portfolio-item-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the item from the portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add users to a portfolio

<a id="opIdaddPortfolioMembers"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/addMembers?members=521621%2C621373 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios/{portfolio_gid}/addMembers</code>
</p>

Adds the specified list of users as members of the portfolio.
Returns the updated portfolio record.

<h3 id="add-users-to-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|members|query|string|true|An array of user ids.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-users-to-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added members to the portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove users from a portfolio

<a id="opIdremovePortfolioMembers"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/removeMembers?members=521621%2C621373 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios/{portfolio_gid}/removeMembers</code>
</p>

Removes the specified list of users from members of the portfolio.
Returns the updated portfolio record.

<h3 id="remove-users-from-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|members|query|string|true|An array of user ids.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-users-from-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the members from the portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a custom field to a portfolio

<a id="opIdportfolio.addCustomFieldSetting"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/addCustomFieldSetting?custom_field=14916 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios/{portfolio_gid}/addCustomFieldSetting</code>
</p>

Custom fields are associated with portfolios by way of custom field settings.  This method creates a setting for the portfolio.

<h3 id="add-a-custom-field-to-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|custom_field|query|string|true|The custom field to associate with this portfolio.|
|is_important|query|boolean|false|Whether this field should be considered important to this portfolio (for instance, to display in the list view of items in the portfolio).|
|insert_before|query|string|false|An id of a Custom Field Setting on this portfolio, before which the new Custom Field Setting will be added.  `insert_before` and `insert_after` parameters cannot both be specified.|
|insert_after|query|string|false|An id of a Custom Field Setting on this portfolio, after which the new Custom Field Setting will be added.  `insert_before` and `insert_after` parameters cannot both be specified.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-a-custom-field-to-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the custom field to the portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a custom field from a portfolio

<a id="opIdportfolio.removeCustomFieldSetting"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/removeCustomFieldSetting?custom_field=14916 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /portfolios/{portfolio_gid}/removeCustomFieldSetting</code>
</p>

Removes a custom field setting from a portfolio.

<h3 id="remove-a-custom-field-from-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|custom_field|query|string|true|The custom field to remove from this portfolio.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-a-custom-field-from-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the custom field from the portfolio.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-portfolio-memberships">Portfolio Memberships</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-portfolio-memberships"><span class="get-verb">GET</span> <span class=""nn>/portfolio_memberships</span></a><br><a href="#get-a-portfolio-membership"><span class="get-verb">GET</span> <span class=""nn>/portfolio_memberships/{portfolio_membership_gid}</span></a><br><a href="#get-memberships-from-a-portfolio"><span class="get-verb">GET</span> <span class=""nn>/portfolios/{portfolio_gid}/portfolio_memberships</span></a></code>
</pre>

This object determines if a user is a member of a portfolio.

<hr class="half-line">
## Get multiple portfolio memberships

<a id="opIdgetPortfolioMemberships"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolio_memberships \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolio_memberships</code>
</p>

Returns a list of portfolio memberships in compact representation. You must specify `portolio`, `portfolio` and `user`, or `workspace` and `user`.

<h3 id="get-multiple-portfolio-memberships-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio|query|string|false|The portfolio to filter results on.|
|workspace|query|string|false|The workspace to filter results on.|
|user|query|string(email)|false|The user to filter results on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "portfolio",
      "name": "Bug Task"
    }
  ]
}
```

<h3 id="get-multiple-portfolio-memberships-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved portfolio memberships.|[Portfolio](#schemaportfolio)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a portfolio membership

<a id="opIdgetPortfolioMembership"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolio_memberships/{portfolio_membership_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolio_memberships/{portfolio_membership_gid}</code>
</p>

Returns the complete portfolio record for a single portfolio membership.

<h3 id="get-a-portfolio-membership-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_membership_path_gid|path|string|true|none|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "portfolio_membership",
    "user": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "portfolio": {
      "gid": "12345",
      "resource_type": "portfolio",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="get-a-portfolio-membership-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested portfolio membership.|[PortfolioMembership](#schemaportfoliomembership)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get memberships from a portfolio

<a id="opIdgetPortfolioMembershipsForPortfolio"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/portfolios/{portfolio_gid}/portfolio_memberships \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /portfolios/{portfolio_gid}/portfolio_memberships</code>
</p>

Returns the compact portfolio membership records for the portfolio.

<h3 id="get-memberships-from-a-portfolio-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|portfolio_gid|path|string|true|Globally unique identifier for the portfolio.|
|user|query|string(email)|false|The user to filter results on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "portfolio_membership",
      "user": {
        ...
      }
    }
  ]
}
```

<h3 id="get-memberships-from-a-portfolio-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested portfolio's memberships.|[PortfolioMembership](#schemaportfoliomembership)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-projects">Projects</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-projects"><span class="get-verb">GET</span> <span class=""nn>/projects</span></a><br><a href="#create-a-project"><span class="post-verb">POST</span> <span class=""nn>/projects</span></a><br><a href="#get-a-project"><span class="get-verb">GET</span> <span class=""nn>/projects/{project_gid}</span></a><br><a href="#update-a-project"><span class="put-verb">PUT</span> <span class=""nn>/projects/{project_gid}</span></a><br><a href="#delete-a-project"><span class="delete-verb">DELETE</span> <span class=""nn>/projects/{project_gid}</span></a><br><a href="#duplicate-a-project"><span class="post-verb">POST</span> <span class=""nn>/projects/{project_gid}/duplicate</span></a><br><a href="#get-projects-a-task-is-in"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/projects</span></a><br><a href="#get-a-team-39-s-projects"><span class="get-verb">GET</span> <span class=""nn>/teams/{team_gid}/projects</span></a><br><a href="#create-a-project-in-a-team"><span class="post-verb">POST</span> <span class=""nn>/teams/{team_gid}/projects</span></a><br><a href="#get-all-projects-in-a-workspace"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/projects</span></a><br><a href="#create-a-project-in-a-workspace"><span class="post-verb">POST</span> <span class=""nn>/workspaces/{workspace_gid}/projects</span></a><br><a href="#add-a-custom-field-to-a-project"><span class="post-verb">POST</span> <span class=""nn>/projects/{project_gid}/addCustomFieldSetting</span></a><br><a href="#remove-a-custom-field-from-a-project"><span class="post-verb">POST</span> <span class=""nn>/projects/{project_gid}/removeCustomFieldSetting</span></a></code>
</pre>

A `project` represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.

Projects in organizations are shared with a single team. You cannot currently change the team of a project via the API. Non-organization workspaces do not have teams and so you should not specify the team of project in a regular workspace.

Followers of a project are a subset of the members of that project. Followers of a project will receive all updates including tasks created, added and removed from that project. Members of the project have access to and will receive status updates of the project. Adding followers to a project will add them as members if they are not already, removing followers from a project will not affect membership.

<hr class="half-line">
## Get multiple projects

<a id="opIdgetProjects"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects</code>
</p>

Returns the compact project records for some filtered set of projects. Use one or more of the parameters provided to filter the projects returned.

<h3 id="get-multiple-projects-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|workspace|query|string|false|The workspace or organization to filter projects on.|
|team|query|string|false|The team to filter projects on.|
|archived|query|boolean|false|Only return projects whose `archived` field takes on the value of this parameter.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy",
      "created_at": "2012-02-22T02:06:58.147Z",
      "archived": false,
      "color": "light-green",
      "current_status": {
        ...
      },
      "custom_fields": [
        ...
      ],
      "custom_field_settings": [
        ...
      ],
      "default_view": "calendar",
      "due_date": "2012-03-26",
      "due_on": "2012-03-26",
      "followers": [
        ...
      ],
      "html_notes": "These are things we need to purchase.",
      "is_template": false,
      "layout": "list",
      "members": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "These are things we need to purchase.",
      "owner": null,
      "public": false,
      "section_migration_status": "not_migrated",
      "start_on": "2012-03-26",
      "team": null,
      "workspace": null
    }
  ]
}
```

<h3 id="get-multiple-projects-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved projects.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a project

<a id="opIdcreateProject"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects</code>
</p>

Create a new project in a workspace or team.

Every project is required to be created in a specific workspace or
organization, and this cannot be changed once set. Note that you can use
the `workspace` parameter regardless of whether or not it is an
organization.

If the workspace for your project is an organization, you must also
supply a `team` to share the project with.

Returns the full record of the newly created project.

> Body parameter

```json
{
  "data": {
    "name": "Bug Project",
    "notes": "For tracking pesky bugs.",
    "workspace": "1331",
    "team": "14916"
  }
}
```

<h3 id="create-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The project to create.|
|» data|body|object|false|none|
|»» name|body|string|false|The name of the project.|
|»» notes|body|string|false|The description of the project.|
|»» workspace|body|string|false|The workspace or organization to create the project in.|
|»» team|body|string|false|If creating in an organization, the specific team to create the project in.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy",
    "created_at": "2012-02-22T02:06:58.147Z",
    "archived": false,
    "color": "light-green",
    "current_status": {
      "color": "green",
      "text": "Everything is great",
      "author": {
        ...
      }
    },
    "custom_fields": [
      {
        ...
      }
    ],
    "custom_field_settings": [
      {
        ...
      }
    ],
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "layout": "list",
    "members": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "section_migration_status": "not_migrated",
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="create-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully retrieved projects.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a project

<a id="opIdgetProject"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects/{project_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects/{project_gid}</code>
</p>

Returns the complete project record for a single project.

<h3 id="get-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy",
    "created_at": "2012-02-22T02:06:58.147Z",
    "archived": false,
    "color": "light-green",
    "current_status": {
      "color": "green",
      "text": "Everything is great",
      "author": {
        ...
      }
    },
    "custom_fields": [
      {
        ...
      }
    ],
    "custom_field_settings": [
      {
        ...
      }
    ],
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "layout": "list",
    "members": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "section_migration_status": "not_migrated",
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="get-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested project.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a project

<a id="opIdupdateProject"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/projects/{project_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /projects/{project_gid}</code>
</p>

A specific, existing project can be updated by making a PUT request on
the URL for that project. Only the fields provided in the `data` block
will be updated; any unspecified fields will remain unchanged.

When using this method, it is best to specify only those fields you wish
to change, or else you may overwrite changes made by another user since
you last retrieved the task.

Returns the complete updated project record.

> Body parameter

```json
{
  "data": {
    "name": "Stuff to buy",
    "archived": false,
    "color": "light-green",
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="update-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ProjectObject](#schemaprojectobject)|true|The updated fields for the project.|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy",
    "created_at": "2012-02-22T02:06:58.147Z",
    "archived": false,
    "color": "light-green",
    "current_status": {
      "color": "green",
      "text": "Everything is great",
      "author": {
        ...
      }
    },
    "custom_fields": [
      {
        ...
      }
    ],
    "custom_field_settings": [
      {
        ...
      }
    ],
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "layout": "list",
    "members": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "section_migration_status": "not_migrated",
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="update-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated the project.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a project

<a id="opIddeleteProject"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/projects/{project_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /projects/{project_gid}</code>
</p>

A specific, existing project can be deleted by making a DELETE request on
the URL for that project.

Returns an empty data record.

<h3 id="delete-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully deleted the specified project.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Duplicate a project

<a id="opIdduplicateProject"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects/{project_gid}/duplicate \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects/{project_gid}/duplicate</code>
</p>

Creates and returns a job that will asynchronously handle the duplication.

> Body parameter

```json
{
  "data": {
    "name": "New Project Name",
    "team": "12345",
    "include": [
      "members",
      "task_notes"
    ],
    "schedule_dates": {
      "should_skip_weekends": true,
      "due_on": "2019-05-21",
      "start_on": "2019-05-21"
    }
  }
}
```

<h3 id="duplicate-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|Describes the duplicate's name and the elements that will be duplicated.|
|» data|body|object|false|none|
|»» name|body|string|true|The name of the new project.|
|»» team|body|string|false|Sets the team of the new project. If team is not defined, the new project will be in the same team as the the original project.|
|»» include|body|string|false|The elements that will be duplicated to the new project. Tasks are always included.|
|»» schedule_dates|body|object|false|A dictionary of options to auto-shift dates. `task_dates` must be included to use this option. Requires either `start_on` or `due_on`, but not both.|
|»»» should_skip_weekends|body|boolean|true|Determines if the auto-shifted dates should skip weekends.|
|»»» due_on|body|string|false|Sets the last due date in the duplicated project to the given date. The rest of the due dates will be offset by the same amount as the due dates in the original project.|
|»»» start_on|body|string|false|Sets the first start date in the duplicated project to the given date. The rest of the start dates will be offset by the same amount as the start dates in the original project.|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Enumerated Values

|Parameter|Value|
|---|---|
| include|members|
| include|notes|
| include|task_notes|
| include|task_assignee|
| include|task_subtasks|
| include|task_attachments|
| include|task_dates|
| include|task_dependencies|
| include|task_followers|
| include|task_tags|
| include|task_projects|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "resource_subtype": "milestone",
    "status": "in_progress",
    "new_project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "new_task": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="duplicate-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the job to handle duplication.|[Job](#schemajob)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get projects a task is in

<a id="opIdgetTaskProjects"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/projects \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/projects</code>
</p>

Returns a compact representation of all of the projects the task is in.

<h3 id="get-projects-a-task-is-in-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy",
      "created_at": "2012-02-22T02:06:58.147Z",
      "archived": false,
      "color": "light-green",
      "current_status": {
        ...
      },
      "custom_fields": [
        ...
      ],
      "custom_field_settings": [
        ...
      ],
      "default_view": "calendar",
      "due_date": "2012-03-26",
      "due_on": "2012-03-26",
      "followers": [
        ...
      ],
      "html_notes": "These are things we need to purchase.",
      "is_template": false,
      "layout": "list",
      "members": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "These are things we need to purchase.",
      "owner": null,
      "public": false,
      "section_migration_status": "not_migrated",
      "start_on": "2012-03-26",
      "team": null,
      "workspace": null
    }
  ]
}
```

<h3 id="get-projects-a-task-is-in-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the projects for the given task.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a team's projects

<a id="opIdgetProjectsInTeam"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/teams/{team_gid}/projects \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /teams/{team_gid}/projects</code>
</p>

Returns the compact project records for all projects in the team.

<h3 id="get-a-team's-projects-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|archived|query|boolean|false|Only return projects whose `archived` field takes on the value of this parameter.|
|team_gid|path|string|true|Globally unique identifier for the team.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy",
      "created_at": "2012-02-22T02:06:58.147Z",
      "archived": false,
      "color": "light-green",
      "current_status": {
        ...
      },
      "custom_fields": [
        ...
      ],
      "custom_field_settings": [
        ...
      ],
      "default_view": "calendar",
      "due_date": "2012-03-26",
      "due_on": "2012-03-26",
      "followers": [
        ...
      ],
      "html_notes": "These are things we need to purchase.",
      "is_template": false,
      "layout": "list",
      "members": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "These are things we need to purchase.",
      "owner": null,
      "public": false,
      "section_migration_status": "not_migrated",
      "start_on": "2012-03-26",
      "team": null,
      "workspace": null
    }
  ]
}
```

<h3 id="get-a-team's-projects-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested team's projects.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a project in a team

<a id="opIdcreateProjectsWithTeam"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/teams/{team_gid}/projects \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /teams/{team_gid}/projects</code>
</p>

Creates a project shared with the given team.

Returns the full record of the newly created project.

> Body parameter

```json
{
  "data": {
    "name": "Stuff to buy",
    "archived": false,
    "color": "light-green",
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="create-a-project-in-a-team-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ProjectObject](#schemaprojectobject)|true|The new project to create.|
|team_gid|path|string|true|Globally unique identifier for the team.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy",
    "created_at": "2012-02-22T02:06:58.147Z",
    "archived": false,
    "color": "light-green",
    "current_status": {
      "color": "green",
      "text": "Everything is great",
      "author": {
        ...
      }
    },
    "custom_fields": [
      {
        ...
      }
    ],
    "custom_field_settings": [
      {
        ...
      }
    ],
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "layout": "list",
    "members": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "section_migration_status": "not_migrated",
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="create-a-project-in-a-team-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the specified project.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get all projects in a workspace

<a id="opIdgetProjectsInWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/projects \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/projects</code>
</p>

Returns the compact project records for all projects in the workspace.

<h3 id="get-all-projects-in-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|archived|query|boolean|false|Only return projects whose `archived` field takes on the value of this parameter.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy",
      "created_at": "2012-02-22T02:06:58.147Z",
      "archived": false,
      "color": "light-green",
      "current_status": {
        ...
      },
      "custom_fields": [
        ...
      ],
      "custom_field_settings": [
        ...
      ],
      "default_view": "calendar",
      "due_date": "2012-03-26",
      "due_on": "2012-03-26",
      "followers": [
        ...
      ],
      "html_notes": "These are things we need to purchase.",
      "is_template": false,
      "layout": "list",
      "members": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "These are things we need to purchase.",
      "owner": null,
      "public": false,
      "section_migration_status": "not_migrated",
      "start_on": "2012-03-26",
      "team": null,
      "workspace": null
    }
  ]
}
```

<h3 id="get-all-projects-in-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested workspace's projects.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a project in a workspace

<a id="opIdcreateProjectsInWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/workspaces/{workspace_gid}/projects \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /workspaces/{workspace_gid}/projects</code>
</p>

Returns the compact project records for all projects in the workspace.

If the workspace for your project is an organization, you must also
supply a team to share the project with.

Returns the full record of the newly created project.

> Body parameter

```json
{
  "data": {
    "name": "Stuff to buy",
    "archived": false,
    "color": "light-green",
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="create-a-project-in-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ProjectObject](#schemaprojectobject)|true|The new project to create.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy",
    "created_at": "2012-02-22T02:06:58.147Z",
    "archived": false,
    "color": "light-green",
    "current_status": {
      "color": "green",
      "text": "Everything is great",
      "author": {
        ...
      }
    },
    "custom_fields": [
      {
        ...
      }
    ],
    "custom_field_settings": [
      {
        ...
      }
    ],
    "default_view": "calendar",
    "due_date": "2012-03-26",
    "due_on": "2012-03-26",
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "These are things we need to purchase.",
    "is_template": false,
    "layout": "list",
    "members": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "These are things we need to purchase.",
    "owner": null,
    "public": false,
    "section_migration_status": "not_migrated",
    "start_on": "2012-03-26",
    "team": null,
    "workspace": null
  }
}
```

<h3 id="create-a-project-in-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created a new project in the specified workspace.|[Project](#schemaproject)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a custom field to a project

<a id="opIdproject.addCustomFieldSetting"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects/{project_gid}/addCustomFieldSetting?custom_field=14916 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects/{project_gid}/addCustomFieldSetting</code>
</p>

Custom fields are associated with projects by way of custom field settings.  This method creates a setting for the project.

<h3 id="add-a-custom-field-to-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|custom_field|query|string|true|The custom field to associate with this project.|
|is_important|query|boolean|false|Whether this field should be considered "important" to this project. This may cause it to be displayed more prominently, for example in the task grid.|
|insert_before|query|string|false|An id of a Custom Field Setting on this project, before which the new Custom Field Setting will be added.  `insert_before` and `insert_after` parameters cannot both be specified.|
|insert_after|query|string|false|An id of a Custom Field Setting on this project, after which the new Custom Field Setting will be added.  `insert_before` and `insert_after` parameters cannot both be specified.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-a-custom-field-to-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the custom field to the project.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a custom field from a project

<a id="opIdproject.removeCustomFieldSetting"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects/{project_gid}/removeCustomFieldSetting?custom_field=14916 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects/{project_gid}/removeCustomFieldSetting</code>
</p>

Removes a custom field setting from a project.

<h3 id="remove-a-custom-field-from-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|custom_field|query|string|true|The custom field to remove from this project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-a-custom-field-from-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the custom field from the project.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-project-memberships">Project Memberships</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-project-membership"><span class="get-verb">GET</span> <span class=""nn>/project_memberships/{project_membership_gid}</span></a><br><a href="#get-memberships-from-a-project"><span class="get-verb">GET</span> <span class=""nn>/projects/{project_gid}/project_memberships</span></a></code>
</pre>

With the introduction of “comment-only” projects in Asana, a user’s membership in a project comes with associated permissions. These permissions (whether a user has full access to the project or comment-only access) are accessible through the project memberships endpoints described here.

<hr class="half-line">
## Get a project membership

<a id="opIdgetProjectMembership"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/project_memberships/{project_membership_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /project_memberships/{project_membership_gid}</code>
</p>

Returns the complete project record for a single project membership.

<h3 id="get-a-project-membership-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_membership_path_gid|path|string|true|none|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project_membership",
    "user": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "write_access": "full_write"
  }
}
```

<h3 id="get-a-project-membership-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested project membership.|[ProjectMembership](#schemaprojectmembership)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get memberships from a project

<a id="opIdgetProjectMembershipsForProject"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects/{project_gid}/project_memberships \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects/{project_gid}/project_memberships</code>
</p>

Returns the compact project membership records for the project.

<h3 id="get-memberships-from-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|user|query|string(email)|false|The user to filter results on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project_membership",
      "user": {
        ...
      }
    }
  ]
}
```

<h3 id="get-memberships-from-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested project's memberships.|[ProjectMembership](#schemaprojectmembership)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-project-statuses">Project Statuses</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-project-status"><span class="get-verb">GET</span> <span class=""nn>/project_statuses/{project_status_gid}</span></a><br><a href="#delete-a-project-status"><span class="delete-verb">DELETE</span> <span class=""nn>/project_statuses/{project_status_gid}</span></a><br><a href="#get-statuses-from-a-project"><span class="get-verb">GET</span> <span class=""nn>/projects/{project_gid}/project_statuses</span></a><br><a href="#create-a-project-status"><span class="post-verb">POST</span> <span class=""nn>/projects/{project_gid}/project_statuses</span></a></code>
</pre>

A *project status* is an update on the progress of a particular project, and is sent out to all project followers when created. These updates include both text describing the update and a color code intended to represent the overall state of the project: “green” for projects that are on track, “yellow” for projects at risk, and “red” for projects that are behind.

Project statuses can be created and deleted, but not modified.

<hr class="half-line">
## Get a project status

<a id="opIdgetProductStatus"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/project_statuses/{project_status_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /project_statuses/{project_status_gid}</code>
</p>

Returns the complete record for a single status update.

<h3 id="get-a-project-status-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_status_path_gid|path|string|true|The project status update to get.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project_status",
    "title": "Status Update - Jun 15",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "text": "The project is moving forward according to plan...",
    "html-text": "'&lt;body&gt;The project &lt;strong&gt;is&lt;/strong&gt; moving forward according to plan...&lt;/body&gt;'",
    "color": "green"
  }
}
```

<h3 id="get-a-project-status-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified project's status updates.|[ProjectStatus](#schemaprojectstatus)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a project status

<a id="opIddeleteProductStatus"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/project_statuses/{project_status_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /project_statuses/{project_status_gid}</code>
</p>

Deletes a specific, existing project status update.

Returns an empty data record.

<h3 id="delete-a-project-status-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_status_path_gid|path|string|true|The project status update to get.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-project-status-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully deleted the specified product status.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get statuses from a project

<a id="opIdgetProductStatuses"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects/{project_gid}/project_statuses \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects/{project_gid}/project_statuses</code>
</p>

Returns the compact project status update records for all updates on the project.

<h3 id="get-statuses-from-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "project_status",
      "title": "Status Update - Jun 15",
      "created_at": "2012-02-22T02:06:58.147Z",
      "created_by": {
        ...
      },
      "text": "The project is moving forward according to plan...",
      "html-text": "'&lt;body&gt;The project &lt;strong&gt;is&lt;/strong&gt; moving forward according to plan...&lt;/body&gt;'",
      "color": "green"
    }
  ]
}
```

<h3 id="get-statuses-from-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified project's status updates.|[ProjectStatus](#schemaprojectstatus)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a project status

<a id="opIdcreateProjectStatus"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects/{project_gid}/project_statuses \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects/{project_gid}/project_statuses</code>
</p>

Creates a new status update on the project.
Returns the full record of the newly created project status update.

> Body parameter

```json
{
  "data": {
    "project": "123456",
    "text": "The project is on track to ship next month!",
    "color": "green"
  }
}
```

<h3 id="create-a-project-status-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The project status to create.|
|» data|body|object|false|none|
|»» project|body|string|true|Globally unique identifier for the project.|
|»» text|body|string|true|The text of the project status update.|
|»» color|body|any|true|The color to associate with the status update.|
|project_gid|path|string|true|Globally unique identifier for the project.|

#### Enumerated Values

|Parameter|Value|
|---|---|
| color|green|
| color|yellow|
| color|red|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "project_status",
    "title": "Status Update - Jun 15",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "text": "The project is moving forward according to plan...",
    "html-text": "'&lt;body&gt;The project &lt;strong&gt;is&lt;/strong&gt; moving forward according to plan...&lt;/body&gt;'",
    "color": "green"
  }
}
```

<h3 id="create-a-project-status-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created a new story.|[ProjectStatus](#schemaprojectstatus)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-sections">Sections</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-section"><span class="get-verb">GET</span> <span class=""nn>/sections/{section_gid}</span></a><br><a href="#update-a-section"><span class="put-verb">PUT</span> <span class=""nn>/sections/{section_gid}</span></a><br><a href="#delete-a-section"><span class="delete-verb">DELETE</span> <span class=""nn>/sections/{section_gid}</span></a><br><a href="#get-sections-in-a-project"><span class="get-verb">GET</span> <span class=""nn>/projects/{project_gid}/sections</span></a><br><a href="#create-a-section-in-a-project"><span class="post-verb">POST</span> <span class=""nn>/projects/{project_gid}/sections</span></a><br><a href="#add-task-to-section"><span class="post-verb">POST</span> <span class=""nn>/sections/{section_gid}/addTask</span></a><br><a href="#move-sections"><span class="post-verb">POST</span> <span class=""nn>/projects/{project_gid}/sections/insert</span></a></code>
</pre>

A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.

Sections are largely a shared idiom in Asana’s API for both list and board views of a project regardless of the project’s layout.

The ‘memberships’ property when [getting a task](#get-a-task) will return the information for the section or the column under ‘section’ in the response.

<hr class="half-line">
## Get a section

<a id="opIdgetSection"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/sections/{section_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /sections/{section_gid}</code>
</p>

Returns the complete record for a single section.

<h3 id="get-a-section-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|section_gid|path|string|true|The globally unique identified for the section.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "section",
    "name": "Next Actions",
    "created_at": "2012-02-22T02:06:58.147Z",
    "projects": [
      {
        ...
      }
    ]
  }
}
```

<h3 id="get-a-section-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved section.|[Section](#schemasection)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a section

<a id="opIdupdateSection"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/sections/{section_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /sections/{section_gid}</code>
</p>

A specific, existing section can be updated by making a PUT request on
the URL for that project. Only the fields provided in the `data` block
will be updated; any unspecified fields will remain unchanged. (note that
at this time, the only field that can be updated is the `name` field.)

When using this method, it is best to specify only those fields you wish
to change, or else you may overwrite changes made by another user since
you last retrieved the task.

Returns the complete updated section record.

> Body parameter

```json
{
  "data": {
    "name": "Next Actions",
    "projects": [
      {
        ...
      }
    ]
  }
}
```

<h3 id="update-a-section-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SectionObject](#schemasectionobject)|true|The section to create.|
|section_gid|path|string|true|The globally unique identified for the section.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "section",
    "name": "Next Actions",
    "created_at": "2012-02-22T02:06:58.147Z",
    "projects": [
      {
        ...
      }
    ]
  }
}
```

<h3 id="update-a-section-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated the specified section.|[Section](#schemasection)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a section

<a id="opIddeleteSection"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/sections/{section_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /sections/{section_gid}</code>
</p>

A specific, existing section can be deleted by making a DELETE request on
the URL for that section.

Note that sections must be empty to be deleted.

The last remaining section in a board view cannot be deleted.

Returns an empty data block.

<h3 id="delete-a-section-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|section_gid|path|string|true|The globally unique identified for the section.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-section-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully deleted the specified section.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get sections in a project

<a id="opIdgetSectionsInProject"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects/{project_gid}/sections \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects/{project_gid}/sections</code>
</p>

Returns the compact records for all sections in the specified project.

<h3 id="get-sections-in-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions",
      "created_at": "2012-02-22T02:06:58.147Z",
      "projects": [
        ...
      ]
    }
  ]
}
```

<h3 id="get-sections-in-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved sections in project.|[Section](#schemasection)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a section in a project

<a id="opIdcreateSectionInProject"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects/{project_gid}/sections \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects/{project_gid}/sections</code>
</p>

Creates a new section in a project.
Returns the full record of the newly created section.

> Body parameter

```json
{
  "data": {
    "project": "13579",
    "name": "Next Actions"
  }
}
```

<h3 id="create-a-section-in-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The section to create.|
|» data|body|object|false|none|
|»» project|body|string|true|The project to create the section in|
|»» name|body|string|true|The text to be displayed as the section name. This cannot be an empty string.|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "section",
    "name": "Next Actions",
    "created_at": "2012-02-22T02:06:58.147Z",
    "projects": [
      {
        ...
      }
    ]
  }
}
```

<h3 id="create-a-section-in-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the specified section.|[Section](#schemasection)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add task to section

<a id="opIdaddTaskToSection"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/sections/{section_gid}/addTask \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /sections/{section_gid}/addTask</code>
</p>

Add a task to a specific, existing section. This is remove the task from other sections of the project.

The task will be inserted at the top of a section unless an insert_before or insert_after parameter is declared.

This does not work for separators (tasks with the resource_subtype of section).

> Body parameter

```json
{
  "data": {
    "task": "123456",
    "insert_before": "86420",
    "insert_after": "987654"
  }
}
```

<h3 id="add-task-to-section-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The task and optionally the insert location.|
|» data|body|object|false|none|
|»» task|body|string|true|The task to add to this section.|
|»» insert_before|body|string|false|An existing task within this section before which the added task should be inserted. Cannot be provided together with insert_after.|
|»» insert_after|body|string|false|An existing task within this section after which the added task should be inserted. Cannot be provided together with insert_before.|
|section_gid|path|string|true|The globally unique identified for the section.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-task-to-section-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Move sections

<a id="opIdmoveSection"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/projects/{project_gid}/sections/insert \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /projects/{project_gid}/sections/insert</code>
</p>

Move sections relative to each other in a board view. One of
`before_section` or `after_section` is required.

Sections cannot be moved between projects.

At this point in time, moving sections is not supported in list views,
only board views.

Returns an empty data block.

> Body parameter

```json
{
  "data": {
    "project": "123456",
    "section": "321654",
    "before_section": "86420",
    "after_section": "987654"
  }
}
```

<h3 id="move-sections-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The section's move action.|
|» data|body|object|false|none|
|»» project|body|string|true|The project in which to reorder the given section.|
|»» section|body|string|true|The section to reorder.|
|»» before_section|body|string|false|Insert the given section immediately before the section specified by this parameter.|
|»» after_section|body|string|false|Insert the given section immediately after the section specified by this parameter.|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="move-sections-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully moved the specified section.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-stories">Stories</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-story"><span class="get-verb">GET</span> <span class=""nn>/stories/{story_gid}</span></a><br><a href="#update-a-story"><span class="put-verb">PUT</span> <span class=""nn>/stories/{story_gid}</span></a><br><a href="#delete-a-story"><span class="delete-verb">DELETE</span> <span class=""nn>/stories/{story_gid}</span></a><br><a href="#get-stories-from-a-task"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/stories</span></a><br><a href="#create-a-comment-on-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/stories</span></a></code>
</pre>

*See [our forum post](https://forum.asana.com/t/no-more-parsing-story-text-new-fields-on-stories/42924) for more info on when conditional fields are returned.*

A *story* represents an activity associated with an object in the Asana system. Stories are generated by the system whenever users take actions such as creating or assigning tasks, or moving tasks between projects. *Comments* are also a form of user-generated story.

<hr class="half-line">
## Get a story

<a id="opIdgetStory"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/stories/{story_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /stories/{story_gid}</code>
</p>

Returns the full record for a single story.

<h3 id="get-a-story-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|story_gid|path|string|true|Globally unique identifier for the story.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "story",
    "resource_subtype": "milestone",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "text": "marked today",
    "type": "comment",
    "html_text": "Get whatever Sashimi has.",
    "is_edited": false,
    "is_pinned": false,
    "hearted": false,
    "hearts": [
      {
        ...
      }
    ],
    "num_hearts": 5,
    "liked": false,
    "likes": [
      {
        ...
      }
    ],
    "num_likes": 5,
    "previews": [
      {
        ...
      }
    ],
    "old_name": "This was the Old Name",
    "new_name": "This is the New Name",
    "old_dates": {
      "start_on": "2019-09-15",
      "due_at": "2012-02-22T02:06:58.158Z",
      "due_on": "2019-09-15"
    },
    "new_dates": {
      "start_on": "2019-09-15",
      "due_at": "2012-02-22T02:06:58.158Z",
      "due_on": "2019-09-15"
    },
    "old_resource_subtype": "default_task",
    "new_resource_subtype": "milestone",
    "story": {
      "gid": "12345",
      "resource_type": "story",
      "resource_subtype": "milestone",
      "created_at": "2012-02-22T02:06:58.147Z",
      "created_by": {
        ...
      },
      "text": "marked today",
      "type": "comment"
    },
    "assignee": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "follower": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "old_section": {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions"
    },
    "new_section": {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions"
    },
    "task": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "tag": {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy"
    },
    "custom_field": {
      "gid": "12345",
      "resource_type": "custom_field",
      "name": "Bug Task",
      "resource_subtype": "milestone",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value"
    },
    "old_text_value": "This was the Old Text",
    "new_text_value": "This is the New Text",
    "old_number_value": 1,
    "new_number_value": 2,
    "old_enum_value": {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "new_enum_value": {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "duplicate_of": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "duplicated_from": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "dependency": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "source": "web",
    "target": {
      "gid": "1234",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="get-a-story-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified story.|[Story](#schemastory)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a story

<a id="opIdupdateStory"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/stories/{story_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /stories/{story_gid}</code>
</p>

Updates the story and returns the full record for the updated story. Only comment stories can have their text updated, and only comment stories and attachment stories can be pinned. Only one of `text` and `html_text` can be specified.

> Body parameter

```json
{
  "data": {
    "text": "marked today",
    "html_text": "Get whatever Sashimi has.",
    "is_pinned": false,
    "old_name": "This was the Old Name",
    "story": {
      "text": "marked today"
    },
    "assignee": {
      "name": "Greg Sanchez"
    },
    "follower": {
      "name": "Greg Sanchez"
    },
    "old_section": {
      "name": "Next Actions"
    },
    "new_section": {
      "name": "Next Actions"
    },
    "task": {
      "name": "Bug Task"
    },
    "project": {
      "name": "Stuff to buy"
    },
    "tag": {
      "name": "Stuff to buy"
    },
    "custom_field": {
      "name": "Bug Task",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value"
    },
    "old_enum_value": {
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "new_enum_value": {
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "duplicate_of": {
      "name": "Bug Task"
    },
    "duplicated_from": {
      "name": "Bug Task"
    },
    "dependency": {
      "name": "Bug Task"
    }
  }
}
```

<h3 id="update-a-story-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[StoryObject](#schemastoryobject)|true|The comment story to update.|
|story_gid|path|string|true|Globally unique identifier for the story.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "story",
    "resource_subtype": "milestone",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "text": "marked today",
    "type": "comment",
    "html_text": "Get whatever Sashimi has.",
    "is_edited": false,
    "is_pinned": false,
    "hearted": false,
    "hearts": [
      {
        ...
      }
    ],
    "num_hearts": 5,
    "liked": false,
    "likes": [
      {
        ...
      }
    ],
    "num_likes": 5,
    "previews": [
      {
        ...
      }
    ],
    "old_name": "This was the Old Name",
    "new_name": "This is the New Name",
    "old_dates": {
      "start_on": "2019-09-15",
      "due_at": "2012-02-22T02:06:58.158Z",
      "due_on": "2019-09-15"
    },
    "new_dates": {
      "start_on": "2019-09-15",
      "due_at": "2012-02-22T02:06:58.158Z",
      "due_on": "2019-09-15"
    },
    "old_resource_subtype": "default_task",
    "new_resource_subtype": "milestone",
    "story": {
      "gid": "12345",
      "resource_type": "story",
      "resource_subtype": "milestone",
      "created_at": "2012-02-22T02:06:58.147Z",
      "created_by": {
        ...
      },
      "text": "marked today",
      "type": "comment"
    },
    "assignee": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "follower": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "old_section": {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions"
    },
    "new_section": {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions"
    },
    "task": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "tag": {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy"
    },
    "custom_field": {
      "gid": "12345",
      "resource_type": "custom_field",
      "name": "Bug Task",
      "resource_subtype": "milestone",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value"
    },
    "old_text_value": "This was the Old Text",
    "new_text_value": "This is the New Text",
    "old_number_value": 1,
    "new_number_value": 2,
    "old_enum_value": {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "new_enum_value": {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "duplicate_of": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "duplicated_from": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "dependency": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "source": "web",
    "target": {
      "gid": "1234",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="update-a-story-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified story.|[Story](#schemastory)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a story

<a id="opIddeleteStory"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/stories/{story_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /stories/{story_gid}</code>
</p>

Deletes a story. A user can only delete stories they have created. Returns an empty data record.

Returns an empty data record.

<h3 id="delete-a-story-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|story_gid|path|string|true|Globally unique identifier for the story.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-story-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully deleted the specified story.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get stories from a task

<a id="opIdgetTaskStories"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/stories \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/stories</code>
</p>

Returns the compact records for all stories on the task.

<h3 id="get-stories-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "story",
      "resource_subtype": "milestone",
      "created_at": "2012-02-22T02:06:58.147Z",
      "created_by": {
        ...
      },
      "text": "marked today",
      "type": "comment",
      "html_text": "Get whatever Sashimi has.",
      "is_edited": false,
      "is_pinned": false,
      "hearted": false,
      "hearts": [
        ...
      ],
      "num_hearts": 5,
      "liked": false,
      "likes": [
        ...
      ],
      "num_likes": 5,
      "previews": [
        ...
      ],
      "old_name": "This was the Old Name",
      "new_name": "This is the New Name",
      "old_dates": {
        ...
      },
      "new_dates": {
        ...
      },
      "old_resource_subtype": "default_task",
      "new_resource_subtype": "milestone",
      "story": {
        ...
      },
      "assignee": {
        ...
      },
      "follower": {
        ...
      },
      "old_section": {
        ...
      },
      "new_section": {
        ...
      },
      "task": {
        ...
      },
      "project": {
        ...
      },
      "tag": {
        ...
      },
      "custom_field": {
        ...
      },
      "old_text_value": "This was the Old Text",
      "new_text_value": "This is the New Text",
      "old_number_value": 1,
      "new_number_value": 2,
      "old_enum_value": {
        ...
      },
      "new_enum_value": {
        ...
      },
      "duplicate_of": {
        ...
      },
      "duplicated_from": {
        ...
      },
      "dependency": {
        ...
      },
      "source": "web",
      "target": {
        ...
      }
    }
  ]
}
```

<h3 id="get-stories-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified task's stories.|[Story](#schemastory)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a comment on a task

<a id="opIdcreateCommentStory"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/stories \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/stories</code>
</p>

Adds a comment to a task. The comment will be authored by the currently
authenticated user, and timestamped when the server receives the
request.

Returns the full record for the new story added to the task.

> Body parameter

```json
{
  "data": {
    "task": "123456",
    "text": "This is a comment."
  }
}
```

<h3 id="create-a-comment-on-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The comment story to create.|
|» data|body|object|false|none|
|»» task|body|string|true|Globally unique identifier for the task.|
|»» text|body|string|true|The plain text of the comment to add.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "story",
    "resource_subtype": "milestone",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "text": "marked today",
    "type": "comment",
    "html_text": "Get whatever Sashimi has.",
    "is_edited": false,
    "is_pinned": false,
    "hearted": false,
    "hearts": [
      {
        ...
      }
    ],
    "num_hearts": 5,
    "liked": false,
    "likes": [
      {
        ...
      }
    ],
    "num_likes": 5,
    "previews": [
      {
        ...
      }
    ],
    "old_name": "This was the Old Name",
    "new_name": "This is the New Name",
    "old_dates": {
      "start_on": "2019-09-15",
      "due_at": "2012-02-22T02:06:58.158Z",
      "due_on": "2019-09-15"
    },
    "new_dates": {
      "start_on": "2019-09-15",
      "due_at": "2012-02-22T02:06:58.158Z",
      "due_on": "2019-09-15"
    },
    "old_resource_subtype": "default_task",
    "new_resource_subtype": "milestone",
    "story": {
      "gid": "12345",
      "resource_type": "story",
      "resource_subtype": "milestone",
      "created_at": "2012-02-22T02:06:58.147Z",
      "created_by": {
        ...
      },
      "text": "marked today",
      "type": "comment"
    },
    "assignee": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "follower": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "old_section": {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions"
    },
    "new_section": {
      "gid": "12345",
      "resource_type": "section",
      "name": "Next Actions"
    },
    "task": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "tag": {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy"
    },
    "custom_field": {
      "gid": "12345",
      "resource_type": "custom_field",
      "name": "Bug Task",
      "resource_subtype": "milestone",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value"
    },
    "old_text_value": "This was the Old Text",
    "new_text_value": "This is the New Text",
    "old_number_value": 1,
    "new_number_value": 2,
    "old_enum_value": {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "new_enum_value": {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    },
    "duplicate_of": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "duplicated_from": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "dependency": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    },
    "source": "web",
    "target": {
      "gid": "1234",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="create-a-comment-on-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created a new story.|[Story](#schemastory)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-tags">Tags</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-tags"><span class="get-verb">GET</span> <span class=""nn>/tags</span></a><br><a href="#create-a-tag"><span class="post-verb">POST</span> <span class=""nn>/tags</span></a><br><a href="#get-a-tag"><span class="get-verb">GET</span> <span class=""nn>/tags/{tag_gid}</span></a><br><a href="#update-a-tag"><span class="put-verb">PUT</span> <span class=""nn>/tags/{tag_gid}</span></a><br><a href="#get-a-task-39-s-tags"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/tags</span></a><br><a href="#get-tags-in-a-workspace"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/tags</span></a><br><a href="#create-a-tag-in-a-workspace"><span class="post-verb">POST</span> <span class=""nn>/workspaces/{workspace_gid}/tags</span></a></code>
</pre>

A tag is a label that can be attached to any task in Asana. It exists in a single workspace or organization.

Tags have some metadata associated with them, but it is possible that we will simplify them in the future so it is not encouraged to rely too heavily on it. Unlike projects, tags do not provide any ordering on the tasks they are associated with.

<hr class="half-line">
## Get multiple tags

<a id="opIdqueryTags"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tags \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tags</code>
</p>

Returns the compact tag records for some filtered set of tags. Use one or more of the parameters provided to filter the tags returned.

<h3 id="get-multiple-tags-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|workspace|query|string|false|The workspace to filter tags on.|
|archived|query|boolean|false|Only return tags whose `archived` field takes on the value of this parameter.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy",
      "followers": [
        ...
      ],
      "color": "light-green",
      "workspace": {
        ...
      }
    }
  ]
}
```

<h3 id="get-multiple-tags-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified set of tags.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a tag

<a id="opIdcreateTag"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tags \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tags</code>
</p>

Creates a new tag in a workspace or organization.

Every tag is required to be created in a specific workspace or
organization, and this cannot be changed once set. Note that you can use
the workspace parameter regardless of whether or not it is an
organization.

Returns the full record of the newly created tag.

> Body parameter

```json
{
  "data": {
    "name": "Stuff to buy",
    "color": "light-green",
    "workspace": {
      "name": "Bug Task"
    }
  }
}
```

<h3 id="create-a-tag-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[TagObject](#schematagobject)|true|The tag to create.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "tag",
    "name": "Stuff to buy",
    "followers": [
      {
        ...
      }
    ],
    "color": "light-green",
    "workspace": {
      "gid": "12345",
      "resource_type": "workspace",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="create-a-tag-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the newly specified tag.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a tag

<a id="opIdgetTag"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tags/{tag_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tags/{tag_gid}</code>
</p>

Returns the complete tag record for a single tag.

<h3 id="get-a-tag-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|tag_gid|path|string|true|Globally unique identifier for the tag.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "tag",
    "name": "Stuff to buy",
    "followers": [
      {
        ...
      }
    ],
    "color": "light-green",
    "workspace": {
      "gid": "12345",
      "resource_type": "workspace",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="get-a-tag-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified tag.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a tag

<a id="opIdupdateTag"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/tags/{tag_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /tags/{tag_gid}</code>
</p>

Updates the properties of a tag. Only the fields provided in the `data`
block will be updated; any unspecified fields will remain unchanged.

When using this method, it is best to specify only those fields you wish
to change, or else you may overwrite changes made by another user since
you last retrieved the task.

Returns the complete updated tag record.

<h3 id="update-a-tag-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|tag_gid|path|string|true|Globally unique identifier for the tag.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "tag",
    "name": "Stuff to buy",
    "followers": [
      {
        ...
      }
    ],
    "color": "light-green",
    "workspace": {
      "gid": "12345",
      "resource_type": "workspace",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="update-a-tag-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated the specified tag.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a task's tags

<a id="opIdgetTaskTags"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/tags \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/tags</code>
</p>

Get a compact representation of all of the tags the task has.

<h3 id="get-a-task's-tags-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy",
      "followers": [
        ...
      ],
      "color": "light-green",
      "workspace": {
        ...
      }
    }
  ]
}
```

<h3 id="get-a-task's-tags-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the tags for the given task.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get tags in a workspace

<a id="opIdqueryAllTagsInWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/tags \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/tags</code>
</p>

Returns the compact tag records for some filtered set of tags. Use one or more of the parameters provided to filter the tags returned.

<h3 id="get-tags-in-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy",
      "followers": [
        ...
      ],
      "color": "light-green",
      "workspace": {
        ...
      }
    }
  ]
}
```

<h3 id="get-tags-in-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified set of tags.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a tag in a workspace

<a id="opIdcreateTagInWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/workspaces/{workspace_gid}/tags \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /workspaces/{workspace_gid}/tags</code>
</p>

Creates a new tag in a workspace or organization.

Every tag is required to be created in a specific workspace or
organization, and this cannot be changed once set. Note that you can use
the workspace parameter regardless of whether or not it is an
organization.

Returns the full record of the newly created tag.

> Body parameter

```json
{
  "data": {
    "name": "Stuff to buy",
    "color": "light-green",
    "workspace": {
      "name": "Bug Task"
    }
  }
}
```

<h3 id="create-a-tag-in-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[TagObject](#schematagobject)|true|The tag to create.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "tag",
      "name": "Stuff to buy",
      "followers": [
        ...
      ],
      "color": "light-green",
      "workspace": {
        ...
      }
    }
  ]
}
```

<h3 id="create-a-tag-in-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified set of tags.|[Tag](#schematag)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-tasks">Tasks</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-tasks"><span class="get-verb">GET</span> <span class=""nn>/tasks</span></a><br><a href="#create-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks</span></a><br><a href="#get-a-task"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}</span></a><br><a href="#update-a-task"><span class="put-verb">PUT</span> <span class=""nn>/tasks/{task_gid}</span></a><br><a href="#delete-a-task"><span class="delete-verb">DELETE</span> <span class=""nn>/tasks/{task_gid}</span></a><br><a href="#duplicate-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/duplicate</span></a><br><a href="#get-tasks-from-a-project"><span class="get-verb">GET</span> <span class=""nn>/projects/{project_gid}/tasks</span></a><br><a href="#get-tasks-from-a-section"><span class="get-verb">GET</span> <span class=""nn>/sections/{section_gid}/tasks</span></a><br><a href="#get-tasks-from-a-tag"><span class="get-verb">GET</span> <span class=""nn>/tags/{tag_gid}/tasks</span></a><br><a href="#get-subtasks-from-a-task"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/subtasks</span></a><br><a href="#create-a-subtask"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/subtasks</span></a><br><a href="#change-the-parent-of-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/setParent</span></a><br><a href="#get-dependencies-from-a-task"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/dependencies</span></a><br><a href="#set-dependencies-for-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/addDependencies</span></a><br><a href="#unlink-dependencies-from-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/removeDependencies</span></a><br><a href="#get-dependents-from-a-task"><span class="get-verb">GET</span> <span class=""nn>/tasks/{task_gid}/dependents</span></a><br><a href="#set-dependents-for-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/addDependents</span></a><br><a href="#unlink-dependents-from-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/removeDependents</span></a><br><a href="#add-a-project-to-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/addProject</span></a><br><a href="#remove-a-project-from-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/removeProject</span></a><br><a href="#add-a-tag-to-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/addTag</span></a><br><a href="#remove-a-tag-from-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/removeTag</span></a><br><a href="#add-followers-to-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/addFollowers</span></a><br><a href="#remove-followers-from-a-task"><span class="post-verb">POST</span> <span class=""nn>/tasks/{task_gid}/removeFollowers</span></a><br><a href="#search-tasks-in-a-workspace"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/tasks/search</span></a></code>
</pre>

The task is the basic object around which many operations in Asana are centered. In the Asana application, multiple tasks populate the middle pane according to some view parameters, and the set of selected tasks determines the more detailed information presented in the details pane.

Sections are unique in that they will be included in the *memberships* field of task objects returned in the API when the task is within a section. They can also be used to manipulate the ordering of a task within a project.

[Queries](#get-a-set-of-tasks) return a compact representation of each object which is typically the id and name fields. Interested in a specific set of fields or all of the fields? Use [field selectors](#input-output-options) to manipulate what data is included in a response.

<hr class="half-line">
## Get multiple tasks

<a id="opIdqueryTasks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks</code>
</p>

Returns the compact task records for some filtered set of tasks. Use one or more of the parameters provided to filter the tasks returned. You must specify a `project` or `tag` if you do not specify `assignee` and `workspace`.

For more complex task retrieval, use [workspaces/{workspace_gid}/tasks/search](#search-tasks-in-a-workspace).

<h3 id="get-multiple-tasks-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|assignee|query|string|false|The assignee to filter tasks on.|
|project|query|string|false|The project to filter tasks on.|
|section|query|string|false|The section to filter tasks on.|
|workspace|query|string|false|The workspace to filter tasks on.|
|completed_since|query|string(date-time)|false|Only return tasks that are either incomplete or that have been completed since this time.|
|modified_since|query|string(date-time)|false|Only return tasks that have been modified since the given time.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Detailed descriptions

**assignee**: The assignee to filter tasks on.
*Note: If you specify `assignee`, you must also specify the `workspace` to filter on.*

**section**: The section to filter tasks on.
*Note: Currently, this is only supported in board views.*

**workspace**: The workspace to filter tasks on.
*Note: If you specify `workspace`, you must also specify the `assignee` to filter on.*

**modified_since**: Only return tasks that have been modified since the given time.

*Note: A task is considered “modified” if any of its properties
change, or associations between it and other objects are modified
(e.g.  a task being added to a project). A task is not considered
modified just because another object it is associated with (e.g. a
subtask) is modified. Actions that count as modifying the task
include assigning, renaming, completing, and adding stories.*

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-multiple-tasks-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved requested tasks.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a task

<a id="opIdcreateTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks</code>
</p>

Creating a new task is as easy as POSTing to the `/tasks` endpoint with a
data block containing the fields you’d like to set on the task. Any
unspecified fields will take on default values.

Every task is required to be created in a specific workspace, and this
workspace cannot be changed once set. The workspace need not be set
explicitly if you specify `projects` or a `parent` task instead.

> Body parameter

```json
{
  "data": {
    "name": "Buy catnip",
    "assignee": "12345",
    "assignee_status": "upcoming",
    "completed": false,
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      "12345"
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "parent": "12345",
    "projects": [
      "12345"
    ],
    "start_on": "2012-03-26",
    "tags": [
      "12345"
    ],
    "workspace": "12345"
  }
}
```

<h3 id="create-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The task to create.|
|» data|body|object|false|The *task* is the basic object around which many operations in Asana are centered.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|Name of the task. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» created_at|body|string(date-time)|false|The time at which this resource was created.|
|»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»» assignee|body|string|false|Gid of an object.|
|»» assignee_status|body|string|false|Scheduling status of this task for the user it is assigned to. This field can only be set if the assignee is non-null.|
|»» completed|body|boolean|false|True if the task is currently marked complete, false if not.|
|»» completed_at|body|string(date-time)¦null|false|The time at which this task was completed, or null if the task is incomplete.|
|»» custom_fields|body|[object]|false|Array of custom field values applied to the project. These represent the custom field values recorded on this project for a particular custom field. For example, these custom field values will contain an `enum_value` property for custom fields of type `enum`, a `string_value` property for custom fields of type `string`, and so on. Please note that the `gid` returned on each custom field value *is identical* to the `gid` of the custom field, which allows referencing the custom field metadata through the `/custom_fields/custom_field-gid` endpoint.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|The name of the object.|
|»»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»»» type|body|string|false|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|»»» enum_options|body|[object]|false|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|The name of the enum option.|
|»»»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»»»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|»»» enum_value|body|any|false|none|
|»»» enabled|body|boolean|false|*Conditional*. Determines if the custom field is enabled or not.|
|»»» text_value|body|string|false|*Conditional*. This string is the value of a text custom field.|
|»»» description|body|string|false|[Opt In](#input-output-options). The description of the custom field.|
|»»» precision|body|integer|false|Only relevant for custom fields of type ‘Number’. This field dictates the number of places after the decimal to round to, i.e. 0 is integer values, 1 rounds to the nearest tenth, and so on. Must be between 0 and 6, inclusive.|
|»»» is_global_to_workspace|body|boolean|false|This flag describes whether this custom field is available to every container in the workspace. Before project-specific custom fields, this field was always true.|
|»»» has_notifications_enabled|body|boolean|false|This flag describes whether a follower of a task with this field should receive inbox notifications from changes to this field.|
|»» dependencies|body|[object]|false|[Opt In](#input-output-options). Array of resources referencing tasks that this task depends on. The objects contain only the gid of the dependency.|
|»»» gid|body|string|false|none|
|»» dependents|body|[object]|false|[Opt In](#input-output-options). Array of resources referencing tasks that depend on this task. The objects contain only the ID of the dependent.|
|»»» gid|body|string|false|none|
|»» due_at|body|string(date)¦null|false|Date and time on which this task is due, or null if the task has no due time. This takes a UTC timestamp and should not be used together with `due_on`.|
|»» due_on|body|string(date)¦null|false|Date on which this task is due, or null if the task has no due date.  This takes a date with `YYYY-MM-DD` format and should not be used together with due_at.|
|»» external|body|object|false|*OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).|
|»»» gid|body|string|false|none|
|»»» data|body|string|false|none|
|»» followers|body|[string]|false|Array of object Gids.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» html_notes|body|string|false|[Opt In](#input-output-options). The notes of the text with formatting as HTML.|
|»» hearted|body|boolean|false|*Deprecated - please use liked instead* True if the task is hearted by the authorized user, false if not.|
|»» hearts|body|[object]|false|*Deprecated - please use likes instead* Array of users who have hearted this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» is_rendered_as_separator|body|boolean|false|[Opt In](#input-output-options). In some contexts tasks can be rendered as a visual separator; for instance, subtasks can appear similar to [sections](#asana-sections) without being true `section` objects. If a `task` object is rendered this way in any context it will have the property `is_rendered_as_separator` set to `true`.<br /><br />*Note: Until the default behavior for our API changes integrations must [opt in to the `new_sections` change] (https://forum.asana.com/t/sections-are-dead-long-live-sections/33951) to modify the `is_rendered_as_separator` property.*|
|»» liked|body|boolean|false|True if the task is liked by the authorized user, false if not.|
|»» likes|body|[object]|false|Array of users who have liked this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» memberships|body|[object]|false|*Create-only*. Array of projects this task is associated with and the section it is in. At task creation time, this array can be used to add the task to specific sections. After task creation, these associations can be modified using the `addProject` and `removeProject` endpoints. Note that over time, more types of memberships may be added to this property.|
|»»» project|body|object|false|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»»» section|body|object|false|A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|The name of the section (i.e. the text displayed as the section header).|
|»» modified_at|body|string(date-time)|false|The time at which this task was last modified.|
|»» notes|body|string|false|More detailed, free-form textual information associated with the task.|
|»» num_hearts|body|integer|false|*Deprecated - please use likes instead* The number of users who have hearted this task.|
|»» num_likes|body|integer|false|The number of users who have liked this task.|
|»» num_subtasks|body|integer|false|[Opt In](#input-output-options). The number of subtasks on this task.|
|»» parent|body|string|false|Gid of an object.|
|»» projects|body|[string]|false|Array of object Gids.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» start_on|body|string(date)¦null|false|The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.|
|»» tags|body|[string]|false|Array of object Gids.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» workspace|body|string|false|Gid of an object.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Detailed descriptions

**resource_subtype**: The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.
The resource_subtype `milestone` represent a single moment in time. This means tasks with this subtype cannot have a start_date.
*Note: The resource_subtype of `section` is under active migration—please see our [forum post](https://forum.asana.com/t/sections-are-dead-long-live-sections) for more information.*

**external**: *OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).
The external field allows you to store app-specific metadata on tasks, including a gid that can be used to retrieve tasks and a data blob that can store app-specific character strings. Note that you will need to authenticate with Oauth to access or modify this data. Once an external gid is set, you can use the notation `external:custom_gid` to reference your object anywhere in the API where you may use the original object gid. See the page on Custom External Data for more details.

**html_notes**: [Opt In](#input-output-options). The notes of the text with formatting as HTML.
*Note: This field is under active migration—please see our blog post for more information.*

**modified_at**: The time at which this task was last modified.

*Note: This does not currently reflect any changes in
associations such as projects or comments that may have been
added or removed from the task.*

**start_on**: The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.
*Note: `due_on` or `due_at` must be present in the request when setting or unsetting the `start_on` parameter.*

#### Enumerated Values

|Parameter|Value|
|---|---|
| resource_subtype|default_task|
| resource_subtype|milestone|
| resource_subtype|section|
| assignee_status|today|
| assignee_status|upcoming|
| assignee_status|later|
| assignee_status|new|
| assignee_status|inbox|
| type|text|
| type|enum|
| type|number|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Buy catnip",
    "created_at": "2012-02-22T02:06:58.147Z",
    "resource_subtype": "default_task",
    "assignee": null,
    "assignee_status": "upcoming",
    "completed": false,
    "completed_at": "2012-02-22T02:06:58.147Z",
    "custom_fields": [
      {
        ...
      }
    ],
    "dependencies": [
      {
        ...
      },
      {
        ...
      }
    ],
    "dependents": [
      {
        ...
      },
      {
        ...
      }
    ],
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "hearted": true,
    "hearts": [
      {
        ...
      }
    ],
    "is_rendered_as_separator": false,
    "liked": true,
    "likes": [
      {
        ...
      }
    ],
    "memberships": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "num_hearts": 5,
    "num_likes": 5,
    "num_subtasks": 3,
    "parent": null,
    "projects": [
      {
        ...
      }
    ],
    "start_on": "2012-03-26",
    "tags": [
      {
        ...
      }
    ],
    "workspace": null
  }
}
```

<h3 id="create-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created a new task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a task

<a id="opIdgetTask"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}</code>
</p>

Returns the complete task record for a single task.

<h3 id="get-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Buy catnip",
    "created_at": "2012-02-22T02:06:58.147Z",
    "resource_subtype": "default_task",
    "assignee": null,
    "assignee_status": "upcoming",
    "completed": false,
    "completed_at": "2012-02-22T02:06:58.147Z",
    "custom_fields": [
      {
        ...
      }
    ],
    "dependencies": [
      {
        ...
      },
      {
        ...
      }
    ],
    "dependents": [
      {
        ...
      },
      {
        ...
      }
    ],
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "hearted": true,
    "hearts": [
      {
        ...
      }
    ],
    "is_rendered_as_separator": false,
    "liked": true,
    "likes": [
      {
        ...
      }
    ],
    "memberships": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "num_hearts": 5,
    "num_likes": 5,
    "num_subtasks": 3,
    "parent": null,
    "projects": [
      {
        ...
      }
    ],
    "start_on": "2012-03-26",
    "tags": [
      {
        ...
      }
    ],
    "workspace": null
  }
}
```

<h3 id="get-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a task

<a id="opIdupdateTask"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/tasks/{task_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /tasks/{task_gid}</code>
</p>

A specific, existing task can be updated by making a PUT request on the
URL for that task. Only the fields provided in the `data` block will be
updated; any unspecified fields will remain unchanged.

When using this method, it is best to specify only those fields you wish
to change, or else you may overwrite changes made by another user since
you last retrieved the task.

Returns the complete updated task record.

> Body parameter

```json
{
  "data": {
    "name": "Buy catnip",
    "assignee": "12345",
    "assignee_status": "upcoming",
    "completed": false,
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "parent": "12345",
    "start_on": "2012-03-26",
    "workspace": null
  }
}
```

<h3 id="update-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The task to update.|
|» data|body|object|false|The *task* is the basic object around which many operations in Asana are centered.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|Name of the task. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» created_at|body|string(date-time)|false|The time at which this resource was created.|
|»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»» assignee|body|string|false|Gid of an object.|
|»» assignee_status|body|string|false|Scheduling status of this task for the user it is assigned to. This field can only be set if the assignee is non-null.|
|»» completed|body|boolean|false|True if the task is currently marked complete, false if not.|
|»» completed_at|body|string(date-time)¦null|false|The time at which this task was completed, or null if the task is incomplete.|
|»» custom_fields|body|[object]|false|Array of custom field values applied to the project. These represent the custom field values recorded on this project for a particular custom field. For example, these custom field values will contain an `enum_value` property for custom fields of type `enum`, a `string_value` property for custom fields of type `string`, and so on. Please note that the `gid` returned on each custom field value *is identical* to the `gid` of the custom field, which allows referencing the custom field metadata through the `/custom_fields/custom_field-gid` endpoint.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|The name of the object.|
|»»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»»» type|body|string|false|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|»»» enum_options|body|[object]|false|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|The name of the enum option.|
|»»»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»»»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|»»» enum_value|body|any|false|none|
|»»» enabled|body|boolean|false|*Conditional*. Determines if the custom field is enabled or not.|
|»»» text_value|body|string|false|*Conditional*. This string is the value of a text custom field.|
|»»» description|body|string|false|[Opt In](#input-output-options). The description of the custom field.|
|»»» precision|body|integer|false|Only relevant for custom fields of type ‘Number’. This field dictates the number of places after the decimal to round to, i.e. 0 is integer values, 1 rounds to the nearest tenth, and so on. Must be between 0 and 6, inclusive.|
|»»» is_global_to_workspace|body|boolean|false|This flag describes whether this custom field is available to every container in the workspace. Before project-specific custom fields, this field was always true.|
|»»» has_notifications_enabled|body|boolean|false|This flag describes whether a follower of a task with this field should receive inbox notifications from changes to this field.|
|»» dependencies|body|[object]|false|[Opt In](#input-output-options). Array of resources referencing tasks that this task depends on. The objects contain only the gid of the dependency.|
|»»» gid|body|string|false|none|
|»» dependents|body|[object]|false|[Opt In](#input-output-options). Array of resources referencing tasks that depend on this task. The objects contain only the ID of the dependent.|
|»»» gid|body|string|false|none|
|»» due_at|body|string(date)¦null|false|Date and time on which this task is due, or null if the task has no due time. This takes a UTC timestamp and should not be used together with `due_on`.|
|»» due_on|body|string(date)¦null|false|Date on which this task is due, or null if the task has no due date.  This takes a date with `YYYY-MM-DD` format and should not be used together with due_at.|
|»» external|body|object|false|*OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).|
|»»» gid|body|string|false|none|
|»»» data|body|string|false|none|
|»» followers|body|[object]|false|Array of users following this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» html_notes|body|string|false|[Opt In](#input-output-options). The notes of the text with formatting as HTML.|
|»» hearted|body|boolean|false|*Deprecated - please use liked instead* True if the task is hearted by the authorized user, false if not.|
|»» hearts|body|[object]|false|*Deprecated - please use likes instead* Array of users who have hearted this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» is_rendered_as_separator|body|boolean|false|[Opt In](#input-output-options). In some contexts tasks can be rendered as a visual separator; for instance, subtasks can appear similar to [sections](#asana-sections) without being true `section` objects. If a `task` object is rendered this way in any context it will have the property `is_rendered_as_separator` set to `true`.<br /><br />*Note: Until the default behavior for our API changes integrations must [opt in to the `new_sections` change] (https://forum.asana.com/t/sections-are-dead-long-live-sections/33951) to modify the `is_rendered_as_separator` property.*|
|»» liked|body|boolean|false|True if the task is liked by the authorized user, false if not.|
|»» likes|body|[object]|false|Array of users who have liked this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» memberships|body|[object]|false|*Create-only*. Array of projects this task is associated with and the section it is in. At task creation time, this array can be used to add the task to specific sections. After task creation, these associations can be modified using the `addProject` and `removeProject` endpoints. Note that over time, more types of memberships may be added to this property.|
|»»» project|body|object|false|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»»» section|body|object|false|A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|The name of the section (i.e. the text displayed as the section header).|
|»» modified_at|body|string(date-time)|false|The time at which this task was last modified.|
|»» notes|body|string|false|More detailed, free-form textual information associated with the task.|
|»» num_hearts|body|integer|false|*Deprecated - please use likes instead* The number of users who have hearted this task.|
|»» num_likes|body|integer|false|The number of users who have liked this task.|
|»» num_subtasks|body|integer|false|[Opt In](#input-output-options). The number of subtasks on this task.|
|»» parent|body|string|false|Gid of an object.|
|»» projects|body|[object]|false|*Create-only.* Array of projects this task is associated with. At task creation time, this array can be used to add the task to many projects at once. After task creation, these associations can be modified using the addProject and removeProject endpoints.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» start_on|body|string(date)¦null|false|The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.|
|»» tags|body|[object]|false|*Create-only*. Array of tags associated with this task. This property may be specified on creation using just an array of tag gids.  In order to change tags on an existing task use `addTag` and `removeTag`.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» workspace|body|any|false|none|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Detailed descriptions

**resource_subtype**: The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.
The resource_subtype `milestone` represent a single moment in time. This means tasks with this subtype cannot have a start_date.
*Note: The resource_subtype of `section` is under active migration—please see our [forum post](https://forum.asana.com/t/sections-are-dead-long-live-sections) for more information.*

**external**: *OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).
The external field allows you to store app-specific metadata on tasks, including a gid that can be used to retrieve tasks and a data blob that can store app-specific character strings. Note that you will need to authenticate with Oauth to access or modify this data. Once an external gid is set, you can use the notation `external:custom_gid` to reference your object anywhere in the API where you may use the original object gid. See the page on Custom External Data for more details.

**html_notes**: [Opt In](#input-output-options). The notes of the text with formatting as HTML.
*Note: This field is under active migration—please see our blog post for more information.*

**modified_at**: The time at which this task was last modified.

*Note: This does not currently reflect any changes in
associations such as projects or comments that may have been
added or removed from the task.*

**start_on**: The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.
*Note: `due_on` or `due_at` must be present in the request when setting or unsetting the `start_on` parameter.*

#### Enumerated Values

|Parameter|Value|
|---|---|
| resource_subtype|default_task|
| resource_subtype|milestone|
| resource_subtype|section|
| assignee_status|today|
| assignee_status|upcoming|
| assignee_status|later|
| assignee_status|new|
| assignee_status|inbox|
| type|text|
| type|enum|
| type|number|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Buy catnip",
    "created_at": "2012-02-22T02:06:58.147Z",
    "resource_subtype": "default_task",
    "assignee": null,
    "assignee_status": "upcoming",
    "completed": false,
    "completed_at": "2012-02-22T02:06:58.147Z",
    "custom_fields": [
      {
        ...
      }
    ],
    "dependencies": [
      {
        ...
      },
      {
        ...
      }
    ],
    "dependents": [
      {
        ...
      },
      {
        ...
      }
    ],
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "hearted": true,
    "hearts": [
      {
        ...
      }
    ],
    "is_rendered_as_separator": false,
    "liked": true,
    "likes": [
      {
        ...
      }
    ],
    "memberships": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "num_hearts": 5,
    "num_likes": 5,
    "num_subtasks": 3,
    "parent": null,
    "projects": [
      {
        ...
      }
    ],
    "start_on": "2012-03-26",
    "tags": [
      {
        ...
      }
    ],
    "workspace": null
  }
}
```

<h3 id="update-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully updated the specified task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a task

<a id="opIddeleteTask"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/tasks/{task_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /tasks/{task_gid}</code>
</p>

A specific, existing task can be deleted by making a DELETE request on
the URL for that task. Deleted tasks go into the “trash” of the user
making the delete request. Tasks can be recovered from the trash within a
period of 30 days; afterward they are completely removed from the system.

Returns an empty data record.

<h3 id="delete-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully deleted the specified task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Duplicate a task

<a id="opIdduplicateTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/duplicate \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/duplicate</code>
</p>

Creates and returns a job that will asynchronously handle the duplication.

> Body parameter

```json
{
  "data": {
    "name": "New Task Name",
    "include": [
      "notes",
      "assignee"
    ]
  }
}
```

<h3 id="duplicate-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|Describes the duplicate's name and the fields that will be duplicated.|
|» data|body|object|false|none|
|»» name|body|string|false|The name of the new task.|
|»» include|body|string|false|The fields that will be duplicated to the new task.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Enumerated Values

|Parameter|Value|
|---|---|
| include|notes|
| include|assignee|
| include|subtasks|
| include|attachments|
| include|tags|
| include|followers|
| include|projects|
| include|dates|
| include|dependencies|
| include|parent|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "resource_subtype": "milestone",
    "status": "in_progress",
    "new_project": {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    },
    "new_task": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    }
  }
}
```

<h3 id="duplicate-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the job to handle duplication.|[Job](#schemajob)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get tasks from a project

<a id="opIdgetProjectTasks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/projects/{project_gid}/tasks \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /projects/{project_gid}/tasks</code>
</p>

Returns the compact task records for all tasks within the given project, ordered by their priority within the project. Tasks can exist in more than one project at a time.

<h3 id="get-tasks-from-a-project-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|project_gid|path|string|true|Globally unique identifier for the project.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-tasks-from-a-project-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested project's tasks.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get tasks from a section

<a id="opIdgetSectionTasks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/sections/{section_gid}/tasks \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /sections/{section_gid}/tasks</code>
</p>

*Board view only*: Returns the compact section records for all tasks within the given section.

<h3 id="get-tasks-from-a-section-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|section_gid|path|string|true|The globally unique identified for the section.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-tasks-from-a-section-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the section's tasks.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get tasks from a tag

<a id="opIdgetTagTasks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tags/{tag_gid}/tasks \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tags/{tag_gid}/tasks</code>
</p>

Returns the compact task records for all tasks with the given tag. Tasks can have more than one tag at a time.

<h3 id="get-tasks-from-a-tag-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|tag_gid|path|string|true|Globally unique identifier for the tag.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-tasks-from-a-tag-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the tasks associated with the specified tag.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get subtasks from a task

<a id="opIdgetSubTasks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/subtasks \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/subtasks</code>
</p>

Returns a compact representation of all of the subtasks of a task.

<h3 id="get-subtasks-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-subtasks-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified task's subtasks.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Create a subtask

<a id="opIdcreateSubtask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/subtasks \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/subtasks</code>
</p>

Creates a new subtask and adds it to the parent task. Returns the full record for the newly created subtask.

> Body parameter

```json
{
  "data": {
    "name": "Buy catnip",
    "assignee": "12345",
    "assignee_status": "upcoming",
    "completed": false,
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      "12345"
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "projects": [
      "12345"
    ],
    "start_on": "2012-03-26",
    "tags": [
      "12345"
    ],
    "workspace": "12345"
  }
}
```

<h3 id="create-a-subtask-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The new subtask to create.|
|» data|body|object|false|The *task* is the basic object around which many operations in Asana are centered.|
|»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»» resource_type|body|string|false|The base type of this resource.|
|»» name|body|string|false|Name of the task. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» created_at|body|string(date-time)|false|The time at which this resource was created.|
|»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»» assignee|body|string|false|Gid of an object.|
|»» assignee_status|body|string|false|Scheduling status of this task for the user it is assigned to. This field can only be set if the assignee is non-null.|
|»» completed|body|boolean|false|True if the task is currently marked complete, false if not.|
|»» completed_at|body|string(date-time)¦null|false|The time at which this task was completed, or null if the task is incomplete.|
|»» custom_fields|body|[object]|false|Array of custom field values applied to the project. These represent the custom field values recorded on this project for a particular custom field. For example, these custom field values will contain an `enum_value` property for custom fields of type `enum`, a `string_value` property for custom fields of type `string`, and so on. Please note that the `gid` returned on each custom field value *is identical* to the `gid` of the custom field, which allows referencing the custom field metadata through the `/custom_fields/custom_field-gid` endpoint.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|The name of the object.|
|»»» resource_subtype|body|string|false|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|»»» type|body|string|false|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|»»» enum_options|body|[object]|false|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|The name of the enum option.|
|»»»» enabled|body|boolean|false|The color of the enum option. Defaults to ‘none’.|
|»»»» color|body|string|false|Whether or not the enum option is a selectable value for the custom field.|
|»»» enum_value|body|any|false|none|
|»»» enabled|body|boolean|false|*Conditional*. Determines if the custom field is enabled or not.|
|»»» text_value|body|string|false|*Conditional*. This string is the value of a text custom field.|
|»»» description|body|string|false|[Opt In](#input-output-options). The description of the custom field.|
|»»» precision|body|integer|false|Only relevant for custom fields of type ‘Number’. This field dictates the number of places after the decimal to round to, i.e. 0 is integer values, 1 rounds to the nearest tenth, and so on. Must be between 0 and 6, inclusive.|
|»»» is_global_to_workspace|body|boolean|false|This flag describes whether this custom field is available to every container in the workspace. Before project-specific custom fields, this field was always true.|
|»»» has_notifications_enabled|body|boolean|false|This flag describes whether a follower of a task with this field should receive inbox notifications from changes to this field.|
|»» dependencies|body|[object]|false|[Opt In](#input-output-options). Array of resources referencing tasks that this task depends on. The objects contain only the gid of the dependency.|
|»»» gid|body|string|false|none|
|»» dependents|body|[object]|false|[Opt In](#input-output-options). Array of resources referencing tasks that depend on this task. The objects contain only the ID of the dependent.|
|»»» gid|body|string|false|none|
|»» due_at|body|string(date)¦null|false|Date and time on which this task is due, or null if the task has no due time. This takes a UTC timestamp and should not be used together with `due_on`.|
|»» due_on|body|string(date)¦null|false|Date on which this task is due, or null if the task has no due date.  This takes a date with `YYYY-MM-DD` format and should not be used together with due_at.|
|»» external|body|object|false|*OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).|
|»»» gid|body|string|false|none|
|»»» data|body|string|false|none|
|»» followers|body|[string]|false|Array of object Gids.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» html_notes|body|string|false|[Opt In](#input-output-options). The notes of the text with formatting as HTML.|
|»» hearted|body|boolean|false|*Deprecated - please use liked instead* True if the task is hearted by the authorized user, false if not.|
|»» hearts|body|[object]|false|*Deprecated - please use likes instead* Array of users who have hearted this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» is_rendered_as_separator|body|boolean|false|[Opt In](#input-output-options). In some contexts tasks can be rendered as a visual separator; for instance, subtasks can appear similar to [sections](#asana-sections) without being true `section` objects. If a `task` object is rendered this way in any context it will have the property `is_rendered_as_separator` set to `true`.<br /><br />*Note: Until the default behavior for our API changes integrations must [opt in to the `new_sections` change] (https://forum.asana.com/t/sections-are-dead-long-live-sections/33951) to modify the `is_rendered_as_separator` property.*|
|»» liked|body|boolean|false|True if the task is liked by the authorized user, false if not.|
|»» likes|body|[object]|false|Array of users who have liked this task.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|*Read-only except when same user as requester*. The user’s name.|
|»» memberships|body|[object]|false|*Create-only*. Array of projects this task is associated with and the section it is in. At task creation time, this array can be used to add the task to specific sections. After task creation, these associations can be modified using the `addProject` and `removeProject` endpoints. Note that over time, more types of memberships may be added to this property.|
|»»» project|body|object|false|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»»» section|body|object|false|A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.|
|»»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»»» resource_type|body|string|false|The base type of this resource.|
|»»»» name|body|string|false|The name of the section (i.e. the text displayed as the section header).|
|»» modified_at|body|string(date-time)|false|The time at which this task was last modified.|
|»» notes|body|string|false|More detailed, free-form textual information associated with the task.|
|»» num_hearts|body|integer|false|*Deprecated - please use likes instead* The number of users who have hearted this task.|
|»» num_likes|body|integer|false|The number of users who have liked this task.|
|»» num_subtasks|body|integer|false|[Opt In](#input-output-options). The number of subtasks on this task.|
|»» parent|body|any|false|none|
|»» projects|body|[string]|false|Array of object Gids.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» start_on|body|string(date)¦null|false|The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.|
|»» tags|body|[string]|false|Array of object Gids.|
|»»» gid|body|string|false|Globally unique identifier of the object, as a string.|
|»»» resource_type|body|string|false|The base type of this resource.|
|»»» name|body|string|false|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|»» workspace|body|string|false|Gid of an object.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Detailed descriptions

**resource_subtype**: The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.
The resource_subtype `milestone` represent a single moment in time. This means tasks with this subtype cannot have a start_date.
*Note: The resource_subtype of `section` is under active migration—please see our [forum post](https://forum.asana.com/t/sections-are-dead-long-live-sections) for more information.*

**external**: *OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).
The external field allows you to store app-specific metadata on tasks, including a gid that can be used to retrieve tasks and a data blob that can store app-specific character strings. Note that you will need to authenticate with Oauth to access or modify this data. Once an external gid is set, you can use the notation `external:custom_gid` to reference your object anywhere in the API where you may use the original object gid. See the page on Custom External Data for more details.

**html_notes**: [Opt In](#input-output-options). The notes of the text with formatting as HTML.
*Note: This field is under active migration—please see our blog post for more information.*

**modified_at**: The time at which this task was last modified.

*Note: This does not currently reflect any changes in
associations such as projects or comments that may have been
added or removed from the task.*

**start_on**: The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.
*Note: `due_on` or `due_at` must be present in the request when setting or unsetting the `start_on` parameter.*

#### Enumerated Values

|Parameter|Value|
|---|---|
| resource_subtype|default_task|
| resource_subtype|milestone|
| resource_subtype|section|
| assignee_status|today|
| assignee_status|upcoming|
| assignee_status|later|
| assignee_status|new|
| assignee_status|inbox|
| type|text|
| type|enum|
| type|number|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Buy catnip",
    "created_at": "2012-02-22T02:06:58.147Z",
    "resource_subtype": "default_task",
    "assignee": null,
    "assignee_status": "upcoming",
    "completed": false,
    "completed_at": "2012-02-22T02:06:58.147Z",
    "custom_fields": [
      {
        ...
      }
    ],
    "dependencies": [
      {
        ...
      },
      {
        ...
      }
    ],
    "dependents": [
      {
        ...
      },
      {
        ...
      }
    ],
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "hearted": true,
    "hearts": [
      {
        ...
      }
    ],
    "is_rendered_as_separator": false,
    "liked": true,
    "likes": [
      {
        ...
      }
    ],
    "memberships": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "num_hearts": 5,
    "num_likes": 5,
    "num_subtasks": 3,
    "parent": null,
    "projects": [
      {
        ...
      }
    ],
    "start_on": "2012-03-26",
    "tags": [
      {
        ...
      }
    ],
    "workspace": null
  }
}
```

<h3 id="create-a-subtask-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the specified subtask.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Change the parent of a task

<a id="opIdchangeSubtaskParent"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/setParent \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/setParent</code>
</p>

parent, or no parent task at all. Returns an empty data block. When using `insert_before` and `insert_after`, at most one of those two options can be specified, and they must already be subtasks of the parent.

> Body parameter

```json
{
  "data": {
    "parent": "987654",
    "insert_after": "null",
    "insert_before": "124816"
  }
}
```

<h3 id="change-the-parent-of-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The new parent of the subtask.|
|» data|body|object|false|none|
|»» parent|body|string|true|The new parent of the task, or `null` for no parent.|
|»» insert_after|body|string|false|A subtask of the parent to insert the task after, or `null` to insert at the beginning of the list.|
|»» insert_before|body|string|false|A subtask of the parent to insert the task before, or `null` to insert at the end of the list.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Buy catnip",
    "created_at": "2012-02-22T02:06:58.147Z",
    "resource_subtype": "default_task",
    "assignee": null,
    "assignee_status": "upcoming",
    "completed": false,
    "completed_at": "2012-02-22T02:06:58.147Z",
    "custom_fields": [
      {
        ...
      }
    ],
    "dependencies": [
      {
        ...
      },
      {
        ...
      }
    ],
    "dependents": [
      {
        ...
      },
      {
        ...
      }
    ],
    "due_at": "2012-02-22T02:06:58.147Z",
    "due_on": "2012-03-26",
    "external": {
      "gid": "my_gid",
      "data": "A blob of information"
    },
    "followers": [
      {
        ...
      }
    ],
    "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
    "hearted": true,
    "hearts": [
      {
        ...
      }
    ],
    "is_rendered_as_separator": false,
    "liked": true,
    "likes": [
      {
        ...
      }
    ],
    "memberships": [
      {
        ...
      }
    ],
    "modified_at": "2012-02-22T02:06:58.147Z",
    "notes": "Mittens really likes the stuff from Humboldt.",
    "num_hearts": 5,
    "num_likes": 5,
    "num_subtasks": 3,
    "parent": null,
    "projects": [
      {
        ...
      }
    ],
    "start_on": "2012-03-26",
    "tags": [
      {
        ...
      }
    ],
    "workspace": null
  }
}
```

<h3 id="change-the-parent-of-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully changed the parent of the specified subtask.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get dependencies from a task

<a id="opIdgetTaskDependencies"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/dependencies \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/dependencies</code>
</p>

Returns the compact representations of all of the dependencies of a task.

<h3 id="get-dependencies-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-dependencies-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified task's dependencies.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Set dependencies for a task

<a id="opIdaddTaskDependencies"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/addDependencies \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/addDependencies</code>
</p>

Marks a set of tasks as dependencies of this task, if they are not already dependencies. *A task can have at most 15 dependencies*.

> Body parameter

```json
{
  "data": {
    "dependencies": [
      "133713",
      "184253"
    ]
  }
}
```

<h3 id="set-dependencies-for-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[DependencyArray](#schemadependencyarray)|true|The list of tasks to set as dependencies.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="set-dependencies-for-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully set the specified dependencies on the task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Unlink dependencies from a task

<a id="opIdremoveTaskDependencies"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/removeDependencies \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/removeDependencies</code>
</p>

Unlinks a set of dependencies from this task.

> Body parameter

```json
{
  "data": {
    "dependencies": [
      "133713",
      "184253"
    ]
  }
}
```

<h3 id="unlink-dependencies-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[DependencyArray](#schemadependencyarray)|true|The list of tasks to unlink as dependencies.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="unlink-dependencies-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully unlinked the dependencies from the specified task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get dependents from a task

<a id="opIdgetTaskDependents"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/tasks/{task_gid}/dependents \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /tasks/{task_gid}/dependents</code>
</p>

Returns the compact representations of all of the dependents of a task.

<h3 id="get-dependents-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-dependents-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the specified dependents of the task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Set dependents for a task

<a id="opIdaddTaskDependents"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/addDependents \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/addDependents</code>
</p>

Marks a set of tasks as dependents of this task, if they are not already dependents. *A task can have at most 30 dependents*.

> Body parameter

```json
{
  "data": {
    "dependents": [
      "133713",
      "184253"
    ]
  }
}
```

<h3 id="set-dependents-for-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[DependentArray](#schemadependentarray)|true|The list of tasks to add as dependents.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="set-dependents-for-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully set the specified dependents on the given task.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Unlink dependents from a task

<a id="opIdremoveTaskDependents"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/removeDependents \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/removeDependents</code>
</p>

Unlinks a set of dependents from this task.

> Body parameter

```json
{
  "data": {
    "dependents": [
      "133713",
      "184253"
    ]
  }
}
```

<h3 id="unlink-dependents-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[DependentArray](#schemadependentarray)|true|The list of tasks to remove as dependents.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="unlink-dependents-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully unlinked the specified tasks as dependents.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a project to a task

<a id="opIdaddProjectToTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/addProject \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/addProject</code>
</p>

Adds the task to the specified project, in the optional location
specified. If no location arguments are given, the task will be added to
the end of the project.

`addProject` can also be used to reorder a task within a project or
section that already contains it.

At most one of `insert_before`, `insert_after`, or `section` should be
specified. Inserting into a section in an non-order-dependent way can be
done by specifying section, otherwise, to insert within a section in a
particular place, specify `insert_before` or `insert_after` and a task
within the section to anchor the position of this task.

Returns an empty data block.

> Body parameter

```json
{
  "data": {
    "project": "13579",
    "insert_after": "124816",
    "insert_before": "432134",
    "section": "987654"
  }
}
```

<h3 id="add-a-project-to-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The project to add the task to.|
|» data|body|object|false|none|
|»» project|body|string|true|The project to add the task to.|
|»» insert_after|body|string¦null|false|A task in the project to insert the task after, or `null` to insert at the beginning of the list.|
|»» insert_before|body|string¦null|false|A task in the project to insert the task before, or `null` to insert at the end of the list.|
|»» section|body|string¦null|false|A section in the project to insert the task into. The task will be inserted at the bottom of the section.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-a-project-to-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the specified project to the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a project from a task

<a id="opIdremoveProjectFromTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/removeProject \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/removeProject</code>
</p>

Removes the task from the specified project. The task will still exist in
the system, but it will not be in the project anymore.

Returns an empty data block.

> Body parameter

```json
{
  "data": {
    "project": "13579"
  }
}
```

<h3 id="remove-a-project-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The project to remove the task from.|
|» data|body|object|false|none|
|»» project|body|string|true|The project to remove the task from.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-a-project-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the specified project from the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a tag to a task

<a id="opIdaddTagToTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/addTag \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/addTag</code>
</p>

Adds a tag to a task. Returns an empty data block.

> Body parameter

```json
{
  "data": {
    "tag": "13579"
  }
}
```

<h3 id="add-a-tag-to-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The tag to add to the task.|
|» data|body|object|false|none|
|»» tag|body|string|true|The tag to add to the task.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-a-tag-to-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the specified tag to the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a tag from a task

<a id="opIdremoveTagFromTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/removeTag \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/removeTag</code>
</p>

Removes a tag from a task. Returns an empty data block.

> Body parameter

```json
{
  "data": {
    "tag": "13579"
  }
}
```

<h3 id="remove-a-tag-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The tag to remove from the task.|
|» data|body|object|false|none|
|»» tag|body|string|true|The tag to remove from the task.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-a-tag-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the specified tag from the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add followers to a task

<a id="opIdaddFollowerToTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/addFollowers \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/addFollowers</code>
</p>

Adds a tag to a task. Returns an empty data block.
Each task can be associated with zero or more followers in the system.
Requests to add/remove followers, if successful, will return the complete updated task record, described above.

> Body parameter

```json
{
  "data": {
    "followers": [
      "13579",
      "321654"
    ]
  }
}
```

<h3 id="add-followers-to-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The tag to add to the task.|
|» data|body|object|false|none|
|»» followers|body|[string]|true|The tag to add to the task.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="add-followers-to-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully added the specified tag to the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove followers from a task

<a id="opIdremoveFollowerToTask"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/tasks/{task_gid}/removeFollowers \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /tasks/{task_gid}/removeFollowers</code>
</p>

Removes each of the specified followers from the task if they are following. Returns the complete, updated record for the affected task.

> Body parameter

```json
{
  "data": {
    "followers": [
      "13579",
      "321654"
    ]
  }
}
```

<h3 id="remove-followers-from-a-task-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The tag to remove to the task.|
|» data|body|object|false|none|
|»» followers|body|[string]|true|The tag to add to the task.|
|task_gid|path|string|true|The task to operate on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-followers-from-a-task-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully removed the specified tag to the task.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Search tasks in a workspace

<a id="opIdgetWorkspaceTasksSearch"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/tasks/search \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/tasks/search</code>
</p>

To mirror the functionality of the Asana web app's advanced search feature, the Asana API has a task search endpoint that allows you to build complex filters to find and retrieve the exact data you need.
#### Custom fields
| Parameter name | Custom field type | Accepted type |
|---|---|---|
| `custom_fields.<id>.is_set` | All | Boolean |
| `custom_fields.<id>.value` | Text | String |
| `custom_fields.<id>.value` | Number | Number |
| `custom_fields.<id>.value` | Enum | Enum option ID |
| `custom_fields.<id>.starts_with` | Text only | String |
| `custom_fields.<id>.ends_with` | Text only | String |
| `custom_fields.<id>.contains` | Text only | String |
| `custom_fields.<id>.less_than` | Number only | Number |
| `custom_fields.<id>.greater_than` | Number only | Number |

For example, if the gid of the custom field is 12345, these query parameter to find tasks where it is set would be `custom_fields.12345.is_set=true`. To match an exact value for an enum custom field, use the gid of the desired enum option and not the name of the enum option: `custom_fields.12345.value=67890`.

Searching for multiple exact matches of a custom field is not supported.
#### Premium access
Like the Asana web product's advance search feature, this search endpoint will only be available to premium Asana users. A user is premium if any of the following is true:

- The workspace in which the search is being performed is a premium workspace - The user is a member of a premium team inside the workspace

Even if a user is only a member of a premium team inside a non-premium workspace, search will allow them to find data anywhere in the workspace, not just inside the premium team. Making a search request using credentials of a non-premium user will result in a `402 Payment Required` error.
#### Pagination
Search results are not stable; repeating the same query multiple times may return the data in a different order, even if the data do not change. Because of this, the traditional [pagination](https://developers.asana.com/docs/#pagination) available elsewhere in the Asana API is not available here. However, you can paginate manually by sorting the search results by their creation time and then modifying each subsequent query to exclude data you have already seen. Page sizes are limited to a maximum of 100 items, and can be specified by the `limit` query parameter.
#### Eventual consistency
Changes in Asana (regardless of whether they’re made though the web product or the API) are forwarded to our search infrastructure to be indexed. This process can take between 10 and 60 seconds to complete under normal operation, and longer during some production incidents. Making a change to a task that would alter its presence in a particular search query will not be reflected immediately. This is also true of the advanced search feature in the web product.
#### Rate limits
You may receive a `429 Too Many Requests` response if you hit any of our [rate limits](https://developers.asana.com/docs/#rate-limits).

<h3 id="search-tasks-in-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|text|query|string|false|Performs full-text search on both task name and description|
|resource_subtype|query|string|false|Filters results by the task's resource_subtype|
|assignee.any|query|string|false|none|
|assignee.not|query|string|false|none|
|assignee_status|query|string|false|none|
|projects.any|query|string|false|none|
|projects.not|query|string|false|none|
|projects.all|query|string|false|none|
|sections.any|query|string|false|none|
|sections.not|query|string|false|none|
|sections.all|query|string|false|none|
|tags.any|query|string|false|none|
|tags.not|query|string|false|none|
|tags.all|query|string|false|none|
|teams.any|query|string|false|none|
|followers.any|query|string|false|none|
|followers.not|query|string|false|none|
|created_by.any|query|string|false|none|
|created_by.not|query|string|false|none|
|assigned_by.any|query|string|false|none|
|assigned_by.not|query|string|false|none|
|liked_by.any|query|string|false|none|
|liked_by.not|query|string|false|none|
|commented_on_by.any|query|string|false|none|
|commented_on_by.not|query|string|false|none|
|due_on.before|query|string(date)|false|none|
|due_on.after|query|string(date)|false|none|
|due_on|query|string(date)|false|none|
|due_at.before|query|string(date-time)|false|none|
|due_at.after|query|string(date-time)|false|none|
|start_on.before|query|string(date)|false|none|
|start_on.after|query|string(date)|false|none|
|start_on|query|string(date)|false|none|
|created_on.before|query|string(date)|false|none|
|created_on.after|query|string(date)|false|none|
|created_on|query|string(date)|false|none|
|created_at.before|query|string(date-time)|false|none|
|created_at.after|query|string(date-time)|false|none|
|completed_on.before|query|string(date)|false|none|
|completed_on.after|query|string(date)|false|none|
|completed_on|query|string(date)|false|none|
|completed_at.before|query|string(date-time)|false|none|
|completed_at.after|query|string(date-time)|false|none|
|modified_on.before|query|string(date)|false|none|
|modified_on.after|query|string(date)|false|none|
|modified_on|query|string(date)|false|none|
|modified_at.before|query|string(date-time)|false|none|
|modified_at.after|query|string(date-time)|false|none|
|is_blocking|query|boolean|false|none|
|is_blocked|query|boolean|false|none|
|has_attachment|query|boolean|false|none|
|completed|query|boolean|false|none|
|is_subtask|query|boolean|false|none|
|sort_by|query|string|false|none|
|sort_ascending|query|boolean|false|none|

#### Enumerated Values

|Parameter|Value|
|---|---|
|resource_subtype|default_task|
|resource_subtype|milestone|
|assignee_status|inbox|
|assignee_status|today|
|assignee_status|upcoming|
|assignee_status|later|
|sort_by|due_date|
|sort_by|created_at|
|sort_by|completed_at|
|sort_by|likes|
|sort_by|modified_at|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="search-tasks-in-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the section's tasks.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-teams">Teams</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-team"><span class="get-verb">GET</span> <span class=""nn>/teams/{team_gid}</span></a><br><a href="#get-teams-in-an-organization"><span class="get-verb">GET</span> <span class=""nn>/organizations/{workspace_gid}/teams</span></a><br><a href="#get-teams-for-a-user"><span class="get-verb">GET</span> <span class=""nn>/users/{user_gid}/teams</span></a><br><a href="#add-a-user-to-a-team"><span class="post-verb">POST</span> <span class=""nn>/teams/{team_gid}/addUser</span></a><br><a href="#remove-a-user-from-a-team"><span class="post-verb">POST</span> <span class=""nn>/teams/{team_gid}/removeUser</span></a></code>
</pre>

A *team* is used to group related projects and people together within an organization. Each project in an organization is associated with a team.

<hr class="half-line">
## Get a team

<a id="opIdgetTeam"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/teams/{team_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /teams/{team_gid}</code>
</p>

Returns the full record for a single team.

<h3 id="get-a-team-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|team_gid|path|string|true|Globally unique identifier for the team.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "team",
    "name": "Bug Task",
    "description": "All developers should be members of this team.",
    "html_description": "<body><em>All</em> developers should be members of this team.</body>",
    "organization": null
  }
}
```

<h3 id="get-a-team-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successsfully retrieved the record for a single team.|[Team](#schemateam)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get teams in an organization

<a id="opIdgetAllTeams"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/organizations/{workspace_gid}/teams \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /organizations/{workspace_gid}/teams</code>
</p>

Returns the compact records for all teams in the organization visible to the authorized user.

<h3 id="get-teams-in-an-organization-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "team",
      "name": "Bug Task",
      "description": "All developers should be members of this team.",
      "html_description": "<body><em>All</em> developers should be members of this team.</body>",
      "organization": null
    }
  ]
}
```

<h3 id="get-teams-in-an-organization-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns the team records for all teams in the organization or workspace accessible to the authenticated user.|[Team](#schemateam)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get teams for a user

<a id="opIdgetTeamsForUser"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/users/{user_gid}/teams?organization_gid=1331 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /users/{user_gid}/teams</code>
</p>

Returns the compact records for all teams to which the given user is assigned.

<h3 id="get-teams-for-a-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|user_gid|path|string|true|Globally unique identifier for the user.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|organization_gid|query|string|true|The workspace or organization to filter teams on.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "team",
      "name": "Bug Task",
      "description": "All developers should be members of this team.",
      "html_description": "<body><em>All</em> developers should be members of this team.</body>",
      "organization": null
    }
  ]
}
```

<h3 id="get-teams-for-a-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns the team records for all teams in the organization or workspace to which the given user is assigned.|[Team](#schemateam)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a user to a team

<a id="opIdaddUserToTeam"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/teams/{team_gid}/addUser \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /teams/{team_gid}/addUser</code>
</p>

The user making this call must be a member of the team in order to add others. The user being added must exist in the same organization as the team.

> Body parameter

```json
{
  "data": {
    "user": "12345"
  }
}
```

<h3 id="add-a-user-to-a-team-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[UserIdObject](#schemauseridobject)|true|The user to add to the team.|
|team_gid|path|string|true|Globally unique identifier for the team.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ]
}
```

<h3 id="add-a-user-to-a-team-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns the full user record for the added user.|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a user from a team

<a id="opIdremoveUserFromTeam"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/teams/{team_gid}/removeUser \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /teams/{team_gid}/removeUser</code>
</p>

The user making this call must be a member of the team in order to remove themselves or others.

> Body parameter

```json
{
  "data": {
    "user": "12345"
  }
}
```

<h3 id="remove-a-user-from-a-team-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[UserIdObject](#schemauseridobject)|true|The user to remove from the team.|
|team_gid|path|string|true|Globally unique identifier for the team.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ]
}
```

<h3 id="remove-a-user-from-a-team-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns an empty data record|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-typeahead">Typeahead</h1>

<pre class="highlight http tab-http">
<code><a href="#get-objects-via-typeahead"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/typeahead</span></a></code>
</pre>

The typeahead search API provides search for objects from a single workspace.

<hr class="half-line">
## Get objects via typeahead

<a id="opIdgetTypeahead"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/typeahead?resource_type=user \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/typeahead</code>
</p>

Retrieves objects in the workspace based via an auto-completion/typeahead
search algorithm. This feature is meant to provide results quickly, so do
not rely on this API to provide extremely accurate search results. The
result set is limited to a single page of results with a maximum size, so
you won’t be able to fetch large numbers of results.

The typeahead search API provides search for objects from a single
workspace. This endpoint should be used to query for objects when
creating an auto-completion/typeahead search feature. This API is meant
to provide results quickly and should not be relied upon for accurate or
exhaustive search results. The results sets are limited in size and
cannot be paginated.

Queries return a compact representation of each object which is typically
the gid and name fields. Interested in a specific set of fields or all of
the fields?! Of course you are. Use field selectors to manipulate what
data is included in a response.

<h3 id="get-objects-via-typeahead-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|resource_type|query|string|true|The type of values the typeahead should return. You can choose from one of the following: `custom_field`, `project`, `tag`, `task`, and `user`. Note that unlike in the names of endpoints, the types listed here are in singular form (e.g. `task`). Using multiple types is not yet supported.|
|type|query|string|false|*Deprecated: new integrations should prefer the resource_type field.*|
|query|query|string|false|The string that will be used to search for relevant objects. If an empty string is passed in, the API will currently return an empty result set.|
|count|query|integer|false|The number of results to return. The default is 20 if this parameter is omitted, with a minimum of 1 and a maximum of 100. If there are fewer results found than requested, all will be returned.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

#### Enumerated Values

|Parameter|Value|
|---|---|
|resource_type|custom_field|
|resource_type|portfolio|
|resource_type|project|
|resource_type|tag|
|resource_type|task|
|resource_type|user|
|type|custom_field|
|type|portfolio|
|type|project|
|type|tag|
|type|task|
|type|user|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task"
    }
  ]
}
```

<h3 id="get-objects-via-typeahead-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved objects via a typeahead search algorithm.|[Asana](#schemaasana)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-users">Users</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-users"><span class="get-verb">GET</span> <span class=""nn>/users</span></a><br><a href="#get-a-user"><span class="get-verb">GET</span> <span class=""nn>/users/{user_gid}</span></a><br><a href="#get-a-user-39-s-favorites"><span class="get-verb">GET</span> <span class=""nn>/users/{user_gid}/favorites</span></a><br><a href="#get-users-in-a-team"><span class="get-verb">GET</span> <span class=""nn>/teams/{team_gid}/users</span></a><br><a href="#get-users-in-a-workspace-or-organization"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/users</span></a></code>
</pre>

A user object represents an account in Asana that can be given access to various workspaces, projects, and tasks.

Like other objects in the system, users are referred to by numerical IDs. However, the special string identifier `me` can be used anywhere a user ID is accepted, to refer to the current authenticated user.

<hr class="half-line">
## Get multiple users

<a id="opIdgetAllUsers"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/users \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /users</code>
</p>

Returns the user records for all users in all workspaces and organizations accessible to the authenticated user. Accepts an optional workspace ID parameter.
Results are sorted by user ID.

<h3 id="get-multiple-users-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace|query|string|false|The workspace or organization ID to filter users on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ]
}
```

<h3 id="get-multiple-users-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested user records.|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a user

<a id="opIdgetUser"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/users/{user_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /users/{user_gid}</code>
</p>

Returns the full user record for the single user with the provided ID.
Results are sorted by user ID.

<h3 id="get-a-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|user_gid|path|string|true|Globally unique identifier for the user.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez",
    "email": "gsanchez@example.com",
    "photo": {
      "image_21x21": "https://...",
      "image_27x27": "https://...",
      "image_36x36": "https://...",
      "image_60x60": "https://...",
      "image_128x128": "https://..."
    },
    "workspaces": [
      {
        ...
      }
    ]
  }
}
```

<h3 id="get-a-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns the user specified.|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a user's favorites

<a id="opIdgetUserFavorites"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/users/{user_gid}/favorites?resource_type=project&workspace=1234 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /users/{user_gid}/favorites</code>
</p>

Returns all of a user's favorites in the given workspace, of the given type.
Results are given in order (The same order as Asana's sidebar).

<h3 id="get-a-user's-favorites-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|user_gid|path|string|true|Globally unique identifier for the user.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|resource_type|query|string|true|The resource type of favorites to be returned.|
|workspace|query|string|true|The workspace in which to get favorites.|

#### Enumerated Values

|Parameter|Value|
|---|---|
|resource_type|portfolio|
|resource_type|project|
|resource_type|tag|
|resource_type|task|
|resource_type|user|

> 200 Response

```json
{
  "gid": "12345",
  "resource_type": "task"
}
```

<h3 id="get-a-user's-favorites-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns the specified user's favorites.|[Asana](#schemaasana)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get users in a team

<a id="opIdgetUsersForTeam"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/teams/{team_gid}/users \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /teams/{team_gid}/users</code>
</p>

Returns the compact records for all users that are members of the team.

<h3 id="get-users-in-a-team-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|team_gid|path|string|true|Globally unique identifier for the team.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ]
}
```

<h3 id="get-users-in-a-team-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Returns the user records for all the members of the team, including guests and limited access users|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get users in a workspace or organization

<a id="opIdgetUsersInWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/users \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/users</code>
</p>

Returns the user records for all users in the specified workspace or organization.
Results are sorted alphabetically by user names.

<h3 id="get-users-in-a-workspace-or-organization-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ]
}
```

<h3 id="get-users-in-a-workspace-or-organization-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Return the users in the specified workspace or org.|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-user-task-lists">User Task Lists</h1>

<pre class="highlight http tab-http">
<code><a href="#get-tasks-from-a-user-task-list"><span class="get-verb">GET</span> <span class=""nn>/user_task_lists/{user_task_list_gid}/tasks</span></a><br><a href="#get-a-user-task-list"><span class="get-verb">GET</span> <span class=""nn>/user_task_list/{user_task_list_gid}</span></a><br><a href="#get-a-user-39-s-task-list"><span class="get-verb">GET</span> <span class=""nn>/users/{user_gid}/user_task_list</span></a></code>
</pre>

A user task list represents the tasks assigned to a particular user.

A user’s “My Tasks” represent all of the tasks assigned to that user. It is visually divided into regions based on the task’s [`assignee_status`](#tocS_Task) for Asana users to triage their tasks based on when they can address them. When building an integration it’s worth noting that tasks with due dates will automatically move through `assignee_status` states as their due dates approach; read up on [task auto-promotion](https://asana.com/guide/help/fundamentals/my-tasks#gl-auto-promote) for more information.

<hr class="half-line">
## Get tasks from a user task list

<a id="opIdgetUserTaskListTasks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/user_task_lists/{user_task_list_gid}/tasks \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /user_task_lists/{user_task_list_gid}/tasks</code>
</p>

Returns the compact list of tasks in a user’s My Tasks list. The returned tasks will be in order within each assignee status group of `Inbox`, `Today`, and `Upcoming`.
*Note: tasks in `Later` have a different ordering in the Asana web app than the other assignee status groups; this endpoint will still return them in list order in `Later` (differently than they show up in Asana, but the same order as in Asana’s mobile apps).*
*Note: Access control is enforced for this endpoint as with all Asana API endpoints, meaning a user’s private tasks will be filtered out if the API-authenticated user does not have access to them.*
*Note: Both complete and incomplete tasks are returned by default unless they are filtered out (for example, setting `completed_since=now` will return only incomplete tasks, which is the default view for “My Tasks” in Asana.)*

<h3 id="get-tasks-from-a-user-task-list-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|completed_since|query|string|false|Only return tasks that are either incomplete or that have been completed since this time. Accepts a date-time string or the keyword *now*.|
|user_task_list_gid|path|string|true|Globally unique identifier for the user task list.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

#### Detailed descriptions

**completed_since**: Only return tasks that are either incomplete or that have been completed since this time. Accepts a date-time string or the keyword *now*.

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Buy catnip",
      "created_at": "2012-02-22T02:06:58.147Z",
      "resource_subtype": "default_task",
      "assignee": null,
      "assignee_status": "upcoming",
      "completed": false,
      "completed_at": "2012-02-22T02:06:58.147Z",
      "custom_fields": [
        ...
      ],
      "dependencies": [
        ...
      ],
      "dependents": [
        ...
      ],
      "due_at": "2012-02-22T02:06:58.147Z",
      "due_on": "2012-03-26",
      "external": {
        ...
      },
      "followers": [
        ...
      ],
      "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
      "hearted": true,
      "hearts": [
        ...
      ],
      "is_rendered_as_separator": false,
      "liked": true,
      "likes": [
        ...
      ],
      "memberships": [
        ...
      ],
      "modified_at": "2012-02-22T02:06:58.147Z",
      "notes": "Mittens really likes the stuff from Humboldt.",
      "num_hearts": 5,
      "num_likes": 5,
      "num_subtasks": 3,
      "parent": null,
      "projects": [
        ...
      ],
      "start_on": "2012-03-26",
      "tags": [
        ...
      ],
      "workspace": null
    }
  ]
}
```

<h3 id="get-tasks-from-a-user-task-list-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the user task list's tasks.|[Task](#schematask)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a user task list

<a id="opIdgetUserTaskList"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/user_task_list/{user_task_list_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /user_task_list/{user_task_list_gid}</code>
</p>

Returns the full record for a user task list.

<h3 id="get-a-user-task-list-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|user_task_list_gid|path|string|true|Globally unique identifier for the user task list.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task",
    "owner": null,
    "workspace": null
  }
}
```

<h3 id="get-a-user-task-list-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the user task list.|[UserTaskList](#schemausertasklist)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a user's task list

<a id="opIdgetUsersTaskList"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/users/{user_gid}/user_task_list \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /users/{user_gid}/user_task_list</code>
</p>

Returns the full record for a user's task list.

<h3 id="get-a-user's-task-list-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|user_gid|path|string|true|Globally unique identifier for the user.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task",
    "owner": null,
    "workspace": null
  }
}
```

<h3 id="get-a-user's-task-list-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the user's task list.|[UserTaskList](#schemausertasklist)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-webhooks">Webhooks</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-webhooks"><span class="get-verb">GET</span> <span class=""nn>/webhooks</span></a><br><a href="#establish-a-webhook"><span class="post-verb">POST</span> <span class=""nn>/webhooks</span></a><br><a href="#get-a-webhook"><span class="get-verb">GET</span> <span class=""nn>/webhooks/{webhook_gid}</span></a><br><a href="#delete-a-webhook"><span class="delete-verb">DELETE</span> <span class=""nn>/webhooks/{webhook_gid}</span></a></code>
</pre>

Webhooks allow an application to be notified of changes. This is in addition to the ability to fetch those changes directly as [Events](#asana-events) - in fact, Webhooks are just a way to receive Events via HTTP POST at the time they occur instead of polling for them. For services accessible via HTTP this is often vastly more convenient, and if events are not too frequent can be significantly more efficient.

In both cases, however, changes are represented as Event objects - refer to the [Events documentation](#asana-events) for more information on what data these events contain.

**NOTE:** While Webhooks send arrays of Event objects to their target, the Event objects themselves contain *only IDs*, rather than the actual resource they are referencing. So while a normal event you receive via GET /events would look like an [Event](/#tocS_Event). In a Webhook payload you will instead receive a [WebhookEvent](#tocS_WebhookEvent) (a simplified version of the event object).

[Webhooks](#tocS_Webhook) themselves contain only the information necessary to deliver the events to the desired target as they are generated.

#### Receiving Events

Because multiple events often happen in short succession, a webhook payload is designed to be able to transmit multiple events at once. The exact model of events is described in the [Events documentation](#asana-events).

The HTTP POST that the target receives contains:

 * An `X-Hook-Signature` header, which allows verifying that the payload
 is genuine.  The signature is a SHA256 HMAC using the shared secret
 (transmitted during the handshake) of the request body. Verification is
 **strongly recommended**, as it would otherwise be possible for an
 attacker to POST a malicious payload to the same endpoint. If the target
 endpoint can be kept secret this risk is mitigated somewhat, of course.
 * A JSON body with a single key, `events`, containing an array of the
 events that have occurred since the last webhook delivery. Note that this
 list may be empty, as periodically we may send a "heartbeat" webhook to
 verify that the endpoint is available.

Note that events are "skinny" - we expect consumers who desire syncing data to make additional calls to the API to retrieve the latest state. Because the data may have already changed by the time we send the event, it would be misleading to send a snapshot of the data along with the event.

#### Error Handling and Retry

If we attempt to send a webhook payload and we receive an error status code, or the request times out, we will retry delivery with exponential backoff. In general, if your servers are not available for an hour, you can expect it to take no longer than approximately an hour after they come back before the paused delivery resumes. However, if we are unable to deliver a message for 24 hours the webhook will be deactivated.

<hr class="half-line">
## Get multiple webhooks

<a id="opIdgetWebhooks"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/webhooks?workspace=1331 \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /webhooks</code>
</p>

Get the compact representation of all webhooks your app has registered for the authenticated user in the given workspace.

<h3 id="get-multiple-webhooks-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|
|workspace|query|string|true|The workspace to query for webhooks in.|
|resource|query|string|false|Only return webhooks for the given resource.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "created_at": "2012-02-22T02:06:58.147Z",
      "active": false,
      "last_failure_at": "2012-02-22T02:06:58.147Z",
      "last_failure_content": "500 Server Error\\n\\nCould not complete the request",
      "last_success_at": "2012-02-22T02:06:58.147Z",
      "resource": null,
      "target": "https://example.com/receive-webhook/7654"
    }
  ]
}
```

<h3 id="get-multiple-webhooks-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested webhooks.|[Webhook](#schemawebhook)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Establish a webhook

<a id="opIdcreateWebhook"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/webhooks \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /webhooks</code>
</p>

Establishing a webhook is a two-part process. First, a simple HTTP POST
similar to any other resource creation. Since you could have multiple
webhooks we recommend specifying a unique local id for each target.

Next comes the confirmation handshake. When a webhook is created, we will
send a test POST to the target with an `X-Hook-Secret` header as
described in the [Resthooks Security
documentation](http://resthooks.org/docs/security/). The target must
respond with a `200 OK` and a matching `X-Hook-Secret` header to confirm
that this webhook subscription is indeed expected.

If you do not acknowledge the webhook’s confirmation handshake it will
fail to setup, and you will receive an error in response to your attempt
to create it. This means you need to be able to receive and complete the
webhook *while* the POST request is in-flight.

```
# Request
curl -H "Authorization: Bearer <personal_access_token>" \
-X POST https://app.asana.com/api/1.0/webhooks \
-d "resource=8675309" \
-d "target=https://example.com/receive-webhook/7654"
```

```
# Handshake sent to https://example.com/
POST /receive-webhook/7654
X-Hook-Secret: b537207f20cbfa02357cf448134da559e8bd39d61597dcd5631b8012eae53e81
```

```
# Handshake response sent by example.com
HTTP/1.1 200
X-Hook-Secret: b537207f20cbfa02357cf448134da559e8bd39d61597dcd5631b8012eae53e81
```

```
# Response
HTTP/1.1 201
{
  "data": {
    "gid": "43214",
    "resource": {
      "gid": "8675309",
      "name": "Bugs"
    },
    "target": "https://example.com/receive-webhook/7654",
    "active": false,
    "last_success_at": null,
    "last_failure_at": null,
    "last_failure_content": null
  }
}
```

> Body parameter

```json
{
  "data": {
    "resource": "12345",
    "target": "https://example.com/receive-webhook/7654"
  }
}
```

<h3 id="establish-a-webhook-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|true|The webhook workspace and target.|
|» data|body|object|false|none|
|»» resource|body|string|true|A resource ID to subscribe to. The resource can be a task or project.|
|»» target|body|string(uri)|true|The URL to receive the HTTP POST.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 201 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "created_at": "2012-02-22T02:06:58.147Z",
    "active": false,
    "last_failure_at": "2012-02-22T02:06:58.147Z",
    "last_failure_content": "500 Server Error\\n\\nCould not complete the request",
    "last_success_at": "2012-02-22T02:06:58.147Z",
    "resource": null,
    "target": "https://example.com/receive-webhook/7654"
  }
}
```

<h3 id="establish-a-webhook-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Successfully created the requested webhook.|[Webhook](#schemawebhook)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a webhook

<a id="opIdgetWebhook"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/webhooks/{webhook_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /webhooks/{webhook_gid}</code>
</p>

Returns the full record for the given webhook.

<h3 id="get-a-webhook-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|webhook_gid|path|string|true|Globally unique identifier for the webhook.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "created_at": "2012-02-22T02:06:58.147Z",
    "active": false,
    "last_failure_at": "2012-02-22T02:06:58.147Z",
    "last_failure_content": "500 Server Error\\n\\nCould not complete the request",
    "last_success_at": "2012-02-22T02:06:58.147Z",
    "resource": null,
    "target": "https://example.com/receive-webhook/7654"
  }
}
```

<h3 id="get-a-webhook-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested webhook.|[Webhook](#schemawebhook)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Delete a webhook

<a id="opIddeleteWebhook"></a>

> Code samples

```shell
# You can also use wget
curl -X DELETE https://app.asana.com/api/1.0/webhooks/{webhook_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="delete-verb">DELETE</span> /webhooks/{webhook_gid}</code>
</p>

This method *permanently* removes a webhook. Note that it may be possible to receive a request that was already in flight after deleting the webhook, but no further requests will be issued.

<h3 id="delete-a-webhook-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|webhook_gid|path|string|true|Globally unique identifier for the webhook.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="delete-a-webhook-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested webhook.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-workspaces">Workspaces</h1>

<pre class="highlight http tab-http">
<code><a href="#get-multiple-workspaces"><span class="get-verb">GET</span> <span class=""nn>/workspaces</span></a><br><a href="#get-a-workspace"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}</span></a><br><a href="#update-a-workspace"><span class="put-verb">PUT</span> <span class=""nn>/workspaces/{workspace_gid}</span></a><br><a href="#add-a-user-to-a-workspace-or-organization"><span class="post-verb">POST</span> <span class=""nn>/workspaces/{workspace_gid}/addUser</span></a><br><a href="#remove-a-user-from-a-workspace-or-organization"><span class="post-verb">POST</span> <span class=""nn>/workspaces/{workspace_gid}/removeUser</span></a></code>
</pre>

A *workspace* is the highest-level organizational unit in Asana. All projects and tasks have an associated workspace.

An *organization* is a special kind of workspace that represents a company. In an organization, you can group your projects into teams. You can read more about how organizations work on the Asana Guide. To tell if your workspace is an organization or not, check its `is_organization` property.

Over time, we intend to migrate most workspaces into organizations and to release more organization-specific functionality. We may eventually deprecate using workspace-based APIs for organizations. Currently, and until after some reasonable grace period following any further announcements, you can still reference organizations in any `workspace` parameter.

<hr class="half-line">
## Get multiple workspaces

<a id="opIdgetAllWorkspaces"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces</code>
</p>

Returns the compact records for all workspaces visible to the authorized user.

<h3 id="get-multiple-workspaces-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task",
      "email_domains": [
        ...
      ],
      "is_organization": false
    }
  ]
}
```

<h3 id="get-multiple-workspaces-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Return all workspaces visible to the authorized user.|[Workspace](#schemaworkspace)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get a workspace

<a id="opIdgetWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}</code>
</p>

Returns the full workspace record for a single workspace.

<h3 id="get-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task",
    "email_domains": [
      "asana.com"
    ],
    "is_organization": false
  }
}
```

<h3 id="get-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Return the full workspace record.|[Workspace](#schemaworkspace)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Update a workspace

<a id="opIdupdateWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X PUT https://app.asana.com/api/1.0/workspaces/{workspace_gid} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="put-verb">PUT</span> /workspaces/{workspace_gid}</code>
</p>

A specific, existing workspace can be updated by making a PUT request on the URL for that workspace. Only the fields provided in the data block will be updated; any unspecified fields will remain unchanged.
Currently the only field that can be modified for a workspace is its name.
Returns the complete, updated workspace record.

> Body parameter

```json
{
  "data": {
    "name": "Bug Task",
    "email_domains": [
      "asana.com"
    ],
    "is_organization": false
  }
}
```

<h3 id="update-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[WorkspaceObject](#schemaworkspaceobject)|true|The workspace object with all updated properties.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task",
    "email_domains": [
      "asana.com"
    ],
    "is_organization": false
  }
}
```

<h3 id="update-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Update for the workspace was successful.|[Workspace](#schemaworkspace)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Add a user to a workspace or organization

<a id="opIdaddUserToWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/workspaces/{workspace_gid}/addUser \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /workspaces/{workspace_gid}/addUser</code>
</p>

Add a user to a workspace or organization.
The user can be referenced by their globally unique user ID or their email address. Returns the full user record for the invited user.

> Body parameter

```json
{
  "data": {
    "user": "12345"
  }
}
```

<h3 id="add-a-user-to-a-workspace-or-organization-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[UserIdObject](#schemauseridobject)|true|The user to add to the workspace.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez",
    "email": "gsanchez@example.com",
    "photo": {
      "image_21x21": "https://...",
      "image_27x27": "https://...",
      "image_36x36": "https://...",
      "image_60x60": "https://...",
      "image_128x128": "https://..."
    },
    "workspaces": [
      {
        ...
      }
    ]
  }
}
```

<h3 id="add-a-user-to-a-workspace-or-organization-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|The user was added successfully to the workspace or organization.|[User](#schemauser)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Remove a user from a workspace or organization

<a id="opIdremoveUserToWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X POST https://app.asana.com/api/1.0/workspaces/{workspace_gid}/removeUser \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="post-verb">POST</span> /workspaces/{workspace_gid}/removeUser</code>
</p>

Remove a user from a workspace or organization.
The user making this call must be an admin in the workspace. The user can be referenced by their globally unique user ID or their email address.
Returns an empty data record.

> Body parameter

```json
{
  "data": {
    "user": "12345"
  }
}
```

<h3 id="remove-a-user-from-a-workspace-or-organization-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[UserIdObject](#schemauseridobject)|true|The user to remove from the workspace.|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {}
}
```

<h3 id="remove-a-user-from-a-workspace-or-organization-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|The user was removed successfully to the workspace or organization.|[Empty](#schemaempty)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="full-line">
<h1 id="asana-workspace-memberships">Workspace Memberships</h1>

<pre class="highlight http tab-http">
<code><a href="#get-a-workspace-membership"><span class="get-verb">GET</span> <span class=""nn>/workspace_memberships/{workspace_membership_gid}</span></a><br><a href="#get-workspace-memberships-for-a-user"><span class="get-verb">GET</span> <span class=""nn>/users/{user_gid}/workspace_memberships</span></a><br><a href="#get-the-workspace-memberships-for-a-workspace"><span class="get-verb">GET</span> <span class=""nn>/workspaces/{workspace_gid}/workspace_memberships</span></a></code>
</pre>

This object determines if a user is a member of a workspace.

<hr class="half-line">
## Get a workspace membership

<a id="opIdgetWorkspaceMembership"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspace_memberships/{workspace_membership_gid} \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspace_memberships/{workspace_membership_gid}</code>
</p>

Returns the complete workspace record for a single workspace membership.

<h3 id="get-a-workspace-membership-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_membership_path_gid|path|string|true|none|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|

> 200 Response

```json
{
  "data": {
    "gid": "12345",
    "resource_type": "workspace_membership",
    "user": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "workspace": {
      "gid": "12345",
      "resource_type": "workspace",
      "name": "Bug Task"
    },
    "user_task_list": {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task",
      "owner": null,
      "workspace": null
    },
    "is_active": true,
    "is_admin": true,
    "is_guest": true
  }
}
```

<h3 id="get-a-workspace-membership-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested workspace membership.|[WorkspaceMembership](#schemaworkspacemembership)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get workspace memberships for a user

<a id="opIdgetWorkspaceMembershipsForUser"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/users/{user_gid}/workspace_memberships \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /users/{user_gid}/workspace_memberships</code>
</p>

Returns the compact workspace membership records for the user.

<h3 id="get-workspace-memberships-for-a-user-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|user_gid|path|string|true|Globally unique identifier for the user.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "workspace_membership",
      "user": {
        ...
      },
      "workspace": {
        ...
      }
    }
  ]
}
```

<h3 id="get-workspace-memberships-for-a-user-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested user's workspace memberships.|[WorkspaceMembership](#schemaworkspacemembership)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|This usually occurs because of a missing or malformed parameter. Check the documentation and the syntax of your request and try again.|[Error](#schemaerror)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|A valid authentication token was not provided with the request, so the API could not associate a user with the request.|[Error](#schemaerror)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The authentication and request syntax was valid but the server is refusing to complete the request. This can happen if you try to read or write to objects or properties that the user does not have access to.|[Error](#schemaerror)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Either the request method and path supplied do not specify a known action in the API, or the object specified by the request does not exist.|[Error](#schemaerror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|There was a problem on Asana’s end. In the event of a server error the response body should contain an error phrase. These phrases can be used by Asana support to quickly look up the incident that caused the server error. Some errors are due to server load, and will not supply an error phrase.|[Error](#schemaerror)|

<hr class="half-line">
## Get the workspace memberships for a workspace

<a id="opIdgetWorkspaceMembershipsForWorkspace"></a>

> Code samples

```shell
# You can also use wget
curl -X GET https://app.asana.com/api/1.0/workspaces/{workspace_gid}/workspace_memberships \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {access-token}'

```

<p>
<code> <span class="get-verb">GET</span> /workspaces/{workspace_gid}/workspace_memberships</code>
</p>

Returns the compact workspace membership records for the workspace.

<h3 id="get-the-workspace-memberships-for-a-workspace-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|workspace_gid|path|string|true|Globally unique identifier for the workspace or organization.|
|user|query|string(email)|false|The user to filter results on.|
|opt_pretty|query|boolean|false|Provides “pretty” output.|
|opt_fields|query|array[string]|false|Defines fields to return.|
|limit|query|integer|false|Results per page.|
|offset|query|string|false|Offset token.|

> 200 Response

```json
{
  "data": [
    {
      "gid": "12345",
      "resource_type": "workspace_membership",
      "user": {
        ...
      },
      "workspace": {
        ...
      }
    }
  ]
}
```

<h3 id="get-the-workspace-memberships-for-a-workspace-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved the requested workspace's memberships.|[WorkspaceMembership](#schemaworkspacemembership)|

<hr class="full-line">

# Schemas

<hr>

<h2 id="tocS_Attachment">Attachment</h2>
<!-- backwards compatibility -->
<a id="schemaattachment"></a>
<a id="schema_Attachment"></a>
<a id="tocSattachment"></a>
<a id="tocsattachment"></a>

```json
{
  "gid": "12345",
  "resource_type": "attachment",
  "name": "Screenshot.png",
  "created_at": "2012-02-22T02:06:58.147Z",
  "download_url": "https://www.dropbox.com/s/123/Screenshot.png?dl=1",
  "host": "dropbox",
  "parent": null,
  "view_url": "https://www.dropbox.com/s/123/Screenshot.png"
}

```

An *attachment* object represents any file attached to a task in Asana, whether it’s an uploaded file or one associated via a third-party service such as Dropbox or Google Drive.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|read-only|The name of the file.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|download_url|string(uri)¦null|false|read-only|The URL containing the content of the attachment.<br>*Note:* May be null if the attachment is hosted by [Box](https://www.box.com/). If present, this URL may only be valid for 1 hour from the time of retrieval. You should avoid persisting this URL somewhere and just refresh it on demand to ensure you do not keep stale URLs.|
|host|string|false|read-only|The service hosting the attachment. Valid values are `asana`, `dropbox`, `gdrive` and `box`.|
|parent|any|false|none|none|
|view_url|string(uri)¦null|false|read-only|The URL where the attachment can be viewed, which may be friendlier to users in a browser than just directing them to a raw file. May be null if no view URL exists for the service.|

<hr>

<h2 id="tocS_AttachmentCompact">AttachmentCompact</h2>
<!-- backwards compatibility -->
<a id="schemaattachmentcompact"></a>
<a id="schema_AttachmentCompact"></a>
<a id="tocSattachmentcompact"></a>
<a id="tocsattachmentcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "attachment",
  "name": "Screenshot.png"
}

```

An *attachment* object represents any file attached to a task in Asana, whether it’s an uploaded file or one associated via a third-party service such as Dropbox or Google Drive.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|read-only|The name of the file.|

<hr>

<h2 id="tocS_BatchRequest">BatchRequest</h2>
<!-- backwards compatibility -->
<a id="schemabatchrequest"></a>
<a id="schema_BatchRequest"></a>
<a id="tocSbatchrequest"></a>
<a id="tocsbatchrequest"></a>

```json
{
  "relative_path": "/tasks/123",
  "method": "get",
  "data": {
    "assignee": "me",
    "workspace": "1337"
  },
  "options": {
    "limit": 3,
    "fields": [
      "name",
      "notes",
      "completed"
    ]
  }
}

```

A request object for use in a batch request.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|relative_path|string|true|none|The path of the desired endpoint relative to the API’s base URL. Query parameters are not accepted here; put them in `data` instead.|
|method|string|true|none|The HTTP method you wish to emulate for the action.|
|data|object|false|none|For `GET` requests, this should be a map of query parameters you would have normally passed in the URL. Options and pagination are not accepted here; put them in `options` instead. For `POST`, `PATCH`, and `PUT` methods, this should be the content you would have normally put in the data field of the body.|
|options|object|false|none|Pagination (`limit` and `offset`) and output options (`fields` or `expand`) for the action. “Pretty” JSON output is not an available option on individual actions; if you want pretty output, specify that option on the parent request.|
|» limit|integer|false|none|Pagination limit for the request.|
|» offset|integer|false|none|Pagination offset for the request.|
|» fields|[string]|false|none|The fields to retrieve in the request.|

#### Enumerated Values

|Property|Value|
|---|---|
|method|get|
|method|post|
|method|put|
|method|delete|
|method|patch|
|method|head|

<hr>

<h2 id="tocS_BatchResult">BatchResult</h2>
<!-- backwards compatibility -->
<a id="schemabatchresult"></a>
<a id="schema_BatchResult"></a>
<a id="tocSbatchresult"></a>
<a id="tocsbatchresult"></a>

```json
{
  "status_code": 200,
  "headers": {
    "location": "/tasks/1234"
  },
  "body": {
    "data": {
      "gid": "1967",
      "completed": false,
      "name": "Hello, world!",
      "notes": "How are you today?"
    }
  }
}

```

A response object returned from a batch request.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status_code|integer|false|none|The HTTP status code that the invoked endpoint returned.|
|headers|object|false|none|A map of HTTP headers specific to this result. This is primarily used for returning a `Location` header to accompany a `201 Created` result.  The parent HTTP response will contain all common headers.|
|body|object|false|none|The JSON body that the invoked endpoint returned.|

<hr>

<h2 id="tocS_CustomField">CustomField</h2>
<!-- backwards compatibility -->
<a id="schemacustomfield"></a>
<a id="schema_CustomField"></a>
<a id="tocScustomfield"></a>
<a id="tocscustomfield"></a>

```json
{
  "gid": "12345",
  "resource_type": "custom_field",
  "name": "Bug Task",
  "resource_subtype": "milestone",
  "type": "text",
  "enum_options": [
    {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    }
  ],
  "enum_value": null,
  "enabled": true,
  "text_value": "Some Value",
  "description": "Development team priority",
  "precision": 2,
  "is_global_to_workspace": true,
  "has_notifications_enabled": true
}

```

Custom Fields store the metadata that is used in order to add user-specified information to tasks in Asana. Be sure to reference the [Custom Fields](#asana-custom-fields) developer documentation for more information about how custom fields relate to various resources in Asana.

Users in Asana can [lock custom fields](https://asana.com/guide/help/premium/custom-fields#gl-lock-fields), which will make them read-only when accessed by other users. Attempting to edit a locked custom field will return HTTP error code `403 Forbidden`.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|
|resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|type|string|false|none|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|enum_options|[object]|false|none|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the enum option.|
|» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|enum_value|any|false|none|none|
|enabled|boolean|false|none|*Conditional*. Determines if the custom field is enabled or not.|
|text_value|string|false|none|*Conditional*. This string is the value of a text custom field.|
|description|string|false|none|[Opt In](#input-output-options). The description of the custom field.|
|precision|integer|false|none|Only relevant for custom fields of type ‘Number’. This field dictates the number of places after the decimal to round to, i.e. 0 is integer values, 1 rounds to the nearest tenth, and so on. Must be between 0 and 6, inclusive.|
|is_global_to_workspace|boolean|false|read-only|This flag describes whether this custom field is available to every container in the workspace. Before project-specific custom fields, this field was always true.|
|has_notifications_enabled|boolean|false|none|This flag describes whether a follower of a task with this field should receive inbox notifications from changes to this field.|

#### Enumerated Values

|Property|Value|
|---|---|
|type|text|
|type|enum|
|type|number|

<hr>

<h2 id="tocS_CustomFieldCompact">CustomFieldCompact</h2>
<!-- backwards compatibility -->
<a id="schemacustomfieldcompact"></a>
<a id="schema_CustomFieldCompact"></a>
<a id="tocScustomfieldcompact"></a>
<a id="tocscustomfieldcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "custom_field",
  "name": "Bug Task",
  "resource_subtype": "milestone",
  "type": "text",
  "enum_options": [
    {
      "gid": "12345",
      "resource_type": "enum_option",
      "name": "Low",
      "enabled": true,
      "color": "blue"
    }
  ],
  "enum_value": null,
  "enabled": true,
  "text_value": "Some Value"
}

```

Custom Fields store the metadata that is used in order to add user-specified information to tasks in Asana. Be sure to reference the [Custom Fields](#asana-custom-fields) developer documentation for more information about how custom fields relate to various resources in Asana.

Users in Asana can [lock custom fields](https://asana.com/guide/help/premium/custom-fields#gl-lock-fields), which will make them read-only when accessed by other users. Attempting to edit a locked custom field will return HTTP error code `403 Forbidden`.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|
|resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|type|string|false|none|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|enum_options|[object]|false|none|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the enum option.|
|» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|enum_value|any|false|none|none|
|enabled|boolean|false|none|*Conditional*. Determines if the custom field is enabled or not.|
|text_value|string|false|none|*Conditional*. This string is the value of a text custom field.|

#### Enumerated Values

|Property|Value|
|---|---|
|type|text|
|type|enum|
|type|number|

<hr>

<h2 id="tocS_CustomFieldSetting">CustomFieldSetting</h2>
<!-- backwards compatibility -->
<a id="schemacustomfieldsetting"></a>
<a id="schema_CustomFieldSetting"></a>
<a id="tocScustomfieldsetting"></a>
<a id="tocscustomfieldsetting"></a>

```json
{
  "gid": "12345",
  "resource_type": "custom_field_setting",
  "project": null,
  "is_important": false,
  "parent": null,
  "custom_field": null
}

```

Custom Fields Settings objects represent the many-to-many join of the Custom Field and Project as well as stores information that is relevant to that particular pairing.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|project|any|false|none|none|
|is_important|boolean|false|read-only|`is_important` is used in the Asana web application to determine if this custom field is displayed in the task list (left pane) of a project. A project can have a maximum of 5 custom field settings marked as `is_important`.|
|parent|any|false|none|none|
|custom_field|any|false|none|none|

<hr>

<h2 id="tocS_CustomFieldSettingCompact">CustomFieldSettingCompact</h2>
<!-- backwards compatibility -->
<a id="schemacustomfieldsettingcompact"></a>
<a id="schema_CustomFieldSettingCompact"></a>
<a id="tocScustomfieldsettingcompact"></a>
<a id="tocscustomfieldsettingcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "custom_field_setting"
}

```

Custom Fields Settings objects represent the many-to-many join of the Custom Field and Project as well as stores information that is relevant to that particular pairing.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|

<hr>

<h2 id="tocS_EnumOption">EnumOption</h2>
<!-- backwards compatibility -->
<a id="schemaenumoption"></a>
<a id="schema_EnumOption"></a>
<a id="tocSenumoption"></a>
<a id="tocsenumoption"></a>

```json
{
  "gid": "12345",
  "resource_type": "enum_option",
  "name": "Low",
  "enabled": true,
  "color": "blue"
}

```

Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.

You can add enum options to a custom field by using the `POST /custom_fields/custom_field_gid/enum_options` endpoint.

**It is not possible to remove or delete an enum option**. Instead, enum options can be disabled by updating the `enabled` field to false with the `PUT /enum_options/enum_option_gid` endpoint. Other attributes can be updated similarly.

On creation of an enum option, `enabled` is always set to `true`, meaning the enum option is a selectable value for the custom field. Setting `enabled=false` is equivalent to “trashing” the enum option in the Asana web app within the “Edit Fields” dialog. The enum option will no longer be selectable but, if the enum option value was previously set within a task, the task will retain the value.

Enum options are an ordered list and by default new enum options are inserted at the end. Ordering in relation to existing enum options can be specified on creation by using `insert_before` or `insert_after` to reference an existing enum option. Only one of `insert_before` and `insert_after` can be provided when creating a new enum option.

An enum options list can be reordered with the `POST /custom_fields/custom_field_gid/enum_options/insert` endpoint.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the enum option.|
|enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|

<hr>

<h2 id="tocS_EnumOptionCompact">EnumOptionCompact</h2>
<!-- backwards compatibility -->
<a id="schemaenumoptioncompact"></a>
<a id="schema_EnumOptionCompact"></a>
<a id="tocSenumoptioncompact"></a>
<a id="tocsenumoptioncompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "enum_option",
  "name": "Low",
  "enabled": true,
  "color": "blue"
}

```

Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.

You can add enum options to a custom field by using the `POST /custom_fields/custom_field_gid/enum_options` endpoint.

**It is not possible to remove or delete an enum option**. Instead, enum options can be disabled by updating the `enabled` field to false with the `PUT /enum_options/enum_option_gid` endpoint. Other attributes can be updated similarly.

On creation of an enum option, `enabled` is always set to `true`, meaning the enum option is a selectable value for the custom field. Setting `enabled=false` is equivalent to “trashing” the enum option in the Asana web app within the “Edit Fields” dialog. The enum option will no longer be selectable but, if the enum option value was previously set within a task, the task will retain the value.

Enum options are an ordered list and by default new enum options are inserted at the end. Ordering in relation to existing enum options can be specified on creation by using `insert_before` or `insert_after` to reference an existing enum option. Only one of `insert_before` and `insert_after` can be provided when creating a new enum option.

An enum options list can be reordered with the `POST /custom_fields/custom_field_gid/enum_options/insert` endpoint.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the enum option.|
|enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|

<hr>

<h2 id="tocS_Error">Error</h2>
<!-- backwards compatibility -->
<a id="schemaerror"></a>
<a id="schema_Error"></a>
<a id="tocSerror"></a>
<a id="tocserror"></a>

```json
{
  "errors": [
    {
      "message": "project: Missing input",
      "help": "For more information on API status codes and how to handle them, read the docs on errors: https://asana.github.io/developer-docs/#errors'",
      "phrase": "6 sad squid snuggle softly"
    }
  ]
}

```

Sadly, sometimes requests to the API are not successful. Failures can
occur for a wide range of reasons. In all cases, the API should return
an HTTP Status Code that indicates the nature of the failure,
with a response body in JSON format containing additional information.

In the event of a server error the response body will contain an error
phrase. These phrases are automatically generated using the
[node-asana-phrase
library](https://github.com/Asana/node-asana-phrase) and can be used by
Asana support to quickly look up the incident that caused the server
error.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|errors|[object]|false|none|none|
|» message|string|false|read-only|Message providing more detail about the error that occurred, if available.|
|» help|string|false|read-only|Additional information directing developers to resources on how to address and fix the problem, if available.|
|» phrase|string|false|read-only|*500 errors only*. A unique error phrase which can be used when contacting developer support to help identify the exact occurrence of the problem in Asana’s logs.|

<hr>

<h2 id="tocS_Event">Event</h2>
<!-- backwards compatibility -->
<a id="schemaevent"></a>
<a id="schema_Event"></a>
<a id="tocSevent"></a>
<a id="tocsevent"></a>

```json
{
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "resource": {
    "gid": "12345",
    "name": "Bug Task"
  },
  "type": "task",
  "action": "changed",
  "parent": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task"
  },
  "created_at": "2012-02-22T02:06:58.147Z"
}

```

An *event* is an object representing a change to a resource that was
observed by an event subscription.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|user|object¦null|false|read-only|The user who triggered the event.<br><br>*Note: The event may be triggered by a different user than the subscriber. For example, if user A subscribes to a task and user B modified it, the event’s user will be user B. Note: Some events are generated by the system, and will have `null` as the user. API consumers should make sure to handle this case.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|resource|object|false|read-only|The resource the event occurred on.<br><br>*Note: The resource that triggered the event may be different from<br>the one that the events were requested for. For example, a<br>subscription to a project will contain events for tasks contained<br>within the project.*|
|» gid|string|false|none|none|
|» name|string|false|none|none|
|type|string|false|read-only|*Deprecated: Refer to the resource_type of the resource.*<br>The type of the resource that generated the event.<br><br>*Note: Currently, only tasks, projects and stories generate<br>events.*|
|action|string|false|read-only|The type of action taken that triggered the event.|
|parent|object¦null|false|read-only|For added/removed events, the parent that resource was added to or removed from. The parent will be `null` for other event types.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|created_at|string(date-time)|false|read-only|The timestamp when the event occurred.|

<hr>

<h2 id="tocS_Job">Job</h2>
<!-- backwards compatibility -->
<a id="schemajob"></a>
<a id="schema_Job"></a>
<a id="tocSjob"></a>
<a id="tocsjob"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "resource_subtype": "milestone",
  "status": "in_progress",
  "new_project": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy"
  },
  "new_task": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task"
  }
}

```

A *job* is an object representing a process that handles asynchronous work.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|status|string|false|read-only|none|
|new_project|object|false|none|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|new_task|object|false|none|The *task* is the basic object around which many operations in Asana are centered.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|

#### Enumerated Values

|Property|Value|
|---|---|
|status|not_started|
|status|in_progress|
|status|completed|
|status|failed|

<hr>

<h2 id="tocS_OrganizationExport">OrganizationExport</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationexport"></a>
<a id="schema_OrganizationExport"></a>
<a id="tocSorganizationexport"></a>
<a id="tocsorganizationexport"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "created_at": "2012-02-22T02:06:58.147Z",
  "download_url": "https://asana-export.s3.amazonaws.com/export-4632784536274-20170127-43246.json.gz?AWSAccessKeyId=xxxxxxxx",
  "state": "started",
  "organization": {
    "gid": "14916",
    "name": "My Workspace"
  }
}

```

An *organization_export* object represents a request to export the complete data of an Organization in JSON format.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|download_url|string(uri)¦null|false|read-only|Download this URL to retreive the full export of the organization<br>in JSON format. It will be compressed in a gzip (.gz) container.<br><br>*Note: May be null if the export is still in progress or<br>failed.  If present, this URL may only be valid for 1 hour from<br>the time of retrieval. You should avoid persisting this URL<br>somewhere and rather refresh on demand to ensure you do not keep<br>stale URLs.*|
|state|string|false|read-only|The current state of the export.|
|organization|object|false|none|*Create-only*: The Organization that is being exported. This can only be specified at create time.|
|» gid|string|false|none|none|
|» name|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|state|pending|
|state|started|
|state|finished|
|state|error|

<hr>

<h2 id="tocS_Portfolio">Portfolio</h2>
<!-- backwards compatibility -->
<a id="schemaportfolio"></a>
<a id="schema_Portfolio"></a>
<a id="tocSportfolio"></a>
<a id="tocsportfolio"></a>

```json
{
  "gid": "12345",
  "resource_type": "portfolio",
  "name": "Bug Task",
  "created_at": "2012-02-22T02:06:58.147Z",
  "created_by": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "color": "light-green",
  "custom_field_settings": [
    {
      "gid": "12345",
      "resource_type": "custom_field_setting",
      "project": null,
      "is_important": false,
      "parent": null,
      "custom_field": null
    }
  ],
  "owner": null,
  "workspace": null,
  "members": null
}

```

A *portfolio* gives a high-level overview of the status of multiple initiatives in Asana. Portfolios provide a dashboard overview of the state of multiple projects, including a progress report and the most recent [project status](#asana-project-statuses) update.
Portfolios have some restrictions on size. Each portfolio has a max of 250 items and, like projects, a max of 20 custom fields.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|created_by|object¦null|false|read-only|The user who created this resource.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|color|string|false|none|Color of the portfolio.|
|custom_field_settings|[object]|false|read-only|Array of custom field settings applied to the portfolio.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» project|any|false|none|none|
|» is_important|boolean|false|read-only|`is_important` is used in the Asana web application to determine if this custom field is displayed in the task list (left pane) of a project. A project can have a maximum of 5 custom field settings marked as `is_important`.|
|» parent|any|false|none|none|
|» custom_field|any|false|none|none|
|owner|any|false|none|none|
|workspace|any|false|none|none|
|members|any|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|color|dark-pink|
|color|dark-green|
|color|dark-blue|
|color|dark-red|
|color|dark-teal|
|color|dark-brown|
|color|dark-orange|
|color|dark-purple|
|color|dark-warm-gray|
|color|light-pink|
|color|light-green|
|color|light-blue|
|color|light-red|
|color|light-teal|
|color|light-brown|
|color|light-orange|
|color|light-purple|
|color|light-warm-gray|

<hr>

<h2 id="tocS_PortfolioCompact">PortfolioCompact</h2>
<!-- backwards compatibility -->
<a id="schemaportfoliocompact"></a>
<a id="schema_PortfolioCompact"></a>
<a id="tocSportfoliocompact"></a>
<a id="tocsportfoliocompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "portfolio",
  "name": "Bug Task"
}

```

A *portfolio* gives a high-level overview of the status of multiple initiatives in Asana. Portfolios provide a dashboard overview of the state of multiple projects, including a progress report and the most recent [project status](#asana-project-statuses) update.
Portfolios have some restrictions on size. Each portfolio has a max of 250 items and, like projects, a max of 20 custom fields.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|

<hr>

<h2 id="tocS_PortfolioMembership">PortfolioMembership</h2>
<!-- backwards compatibility -->
<a id="schemaportfoliomembership"></a>
<a id="schema_PortfolioMembership"></a>
<a id="tocSportfoliomembership"></a>
<a id="tocsportfoliomembership"></a>

```json
{
  "gid": "12345",
  "resource_type": "portfolio_membership",
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "portfolio": {
    "gid": "12345",
    "resource_type": "portfolio",
    "name": "Bug Task"
  }
}

```

This object determines if a user is a member of a portfolio.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|user|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|portfolio|object|false|none|A *portfolio* gives a high-level overview of the status of multiple initiatives in Asana. Portfolios provide a dashboard overview of the state of multiple projects, including a progress report and the most recent [project status](#asana-project-statuses) update.<br>Portfolios have some restrictions on size. Each portfolio has a max of 250 items and, like projects, a max of 20 custom fields.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|

<hr>

<h2 id="tocS_PortfolioMembershipCompact">PortfolioMembershipCompact</h2>
<!-- backwards compatibility -->
<a id="schemaportfoliomembershipcompact"></a>
<a id="schema_PortfolioMembershipCompact"></a>
<a id="tocSportfoliomembershipcompact"></a>
<a id="tocsportfoliomembershipcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "portfolio_membership",
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  }
}

```

This object determines if a user is a member of a portfolio.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|user|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|

<hr>

<h2 id="tocS_Preview">Preview</h2>
<!-- backwards compatibility -->
<a id="schemapreview"></a>
<a id="schema_Preview"></a>
<a id="tocSpreview"></a>
<a id="tocspreview"></a>

```json
{
  "fallback": "Greg: Great! I like this idea.\\n\\nhttps//a_company.slack.com/archives/ABCDEFG/12345678",
  "footer": "Mar 17, 2019 1:25 PM",
  "header": "Asana for Slack",
  "header_link": "https://asana.comn/apps/slack",
  "html_text": "<body>Great! I like this idea.</body>",
  "text": "Great! I like this idea.",
  "title": "Greg",
  "title_link": "https://asana.slack.com/archives/ABCDEFG/12345678"
}

```

A collection of rich text that will be displayed as a preview to another app.

This is read-only except for a small group of whitelisted apps.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|fallback|string|false|none|Some fallback text to display if unable to display the full preview.|
|footer|string|false|none|Text to display in the footer.|
|header|string|false|none|Text to display in the header.|
|header_link|string|false|none|Where the header will link to.|
|html_text|string|false|none|HTML formatted text for the body of the preview.|
|text|string|false|none|Text for the body of the preview.|
|title|string|false|none|Text to display as the title.|
|title_link|string|false|none|Where to title will link to.|

<hr>

<h2 id="tocS_Project">Project</h2>
<!-- backwards compatibility -->
<a id="schemaproject"></a>
<a id="schema_Project"></a>
<a id="tocSproject"></a>
<a id="tocsproject"></a>

```json
{
  "gid": "12345",
  "resource_type": "project",
  "name": "Stuff to buy",
  "created_at": "2012-02-22T02:06:58.147Z",
  "archived": false,
  "color": "light-green",
  "current_status": {
    "color": "green",
    "text": "Everything is great",
    "author": {
      "gid": "12345",
      "name": "Greg Bizarro"
    }
  },
  "custom_fields": [
    {
      "gid": "12345",
      "resource_type": "custom_field",
      "name": "Bug Task",
      "resource_subtype": "milestone",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value"
    }
  ],
  "custom_field_settings": [
    {
      "gid": "12345",
      "resource_type": "custom_field_setting"
    }
  ],
  "default_view": "calendar",
  "due_date": "2012-03-26",
  "due_on": "2012-03-26",
  "followers": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    }
  ],
  "html_notes": "These are things we need to purchase.",
  "is_template": false,
  "layout": "list",
  "members": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    }
  ],
  "modified_at": "2012-02-22T02:06:58.147Z",
  "notes": "These are things we need to purchase.",
  "owner": null,
  "public": false,
  "section_migration_status": "not_migrated",
  "start_on": "2012-03-26",
  "team": null,
  "workspace": null
}

```

A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|archived|boolean|false|none|True if the project is archived, false if not. Archived projects do not show in the UI by default and may be treated differently for queries.|
|color|string¦null|false|none|Color of the project.|
|current_status|object¦null|false|read-only|The most recently created status update for the project, or `null` if no update exists. See also the documentation for [project status updates](#asana-project-statuses).|
|» color|string|false|none|none|
|» text|string|false|none|none|
|» author|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|custom_fields|[object]|false|read-only|Array of Custom Fields.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|» resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|» type|string|false|none|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|» enum_options|[object]|false|none|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|The name of the enum option.|
|»» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|»» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|» enum_value|any|false|none|none|
|» enabled|boolean|false|none|*Conditional*. Determines if the custom field is enabled or not.|
|» text_value|string|false|none|*Conditional*. This string is the value of a text custom field.|
|custom_field_settings|[object]|false|read-only|Array of Custom Field Settings (in compact form).|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|default_view|string|false|none|The default view (list, board, calendar, or timeline) of a project.|
|due_date|string(date-time)¦null|false|none|*Deprecated: new integrations should prefer the due_on field.*|
|due_on|string(date-time)¦null|false|none|The day on which this project is due. This takes a date with format YYYY-MM-DD.|
|followers|[object]|false|read-only|Array of users following this project. Followers are a subset of members who receive all notifications for a project, the default notification setting when adding members to a project in-product.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|html_notes|string|false|none|[Opt In](#input-output-options). The notes of the project with formatting as HTML.<br>*Note: This field is under active migration—please see our [blog post] (https://developers.asana.com/docs/#rich-text) for more information.*|
|is_template|boolean|false|none|[Opt In](#input-output-options). Determines if the project is a template.|
|layout|string|false|read-only|The layout (board or list view) of a project|
|members|[object]|false|read-only|Array of users who are members of this project.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|modified_at|string(date-time)|false|read-only|The time at which this project was last modified.<br>*Note: This does not currently reflect any changes in associations such as tasks or comments that may have been added or removed from the project.*|
|notes|string|false|none|More detailed, free-form textual information associated with the project.|
|owner|any|false|none|none|
|public|boolean|false|none|True if the project is public to the organization. If false, do not share this project with other users in this organization without explicitly checking to see if they have access.|
|section_migration_status|string|false|read-only|*Read-only* The section migration status of this project.|
|start_on|string(date)¦null|false|none|The day on which work for this project begins, or null if the project has no start date. This takes a date with `YYYY-MM-DD` format. *Note: `due_on` or `due_at` must be present in the request when setting or unsetting the `start_on` parameter.*|
|team|any|false|none|none|
|workspace|any|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|color|dark-pink|
|color|dark-green|
|color|dark-blue|
|color|dark-red|
|color|dark-teal|
|color|dark-brown|
|color|dark-orange|
|color|dark-purple|
|color|dark-warm-gray|
|color|light-pink|
|color|light-green|
|color|light-blue|
|color|light-red|
|color|light-teal|
|color|light-brown|
|color|light-orange|
|color|light-purple|
|color|light-warm-gray|
|color|green|
|color|yellow|
|color|red|
|type|text|
|type|enum|
|type|number|
|default_view|list|
|default_view|board|
|default_view|calendar|
|default_view|timeline|
|layout|list|
|layout|board|
|section_migration_status|not_migrated|
|section_migration_status|in_progress|
|section_migration_status|completed|

<hr>

<h2 id="tocS_ProjectCompact">ProjectCompact</h2>
<!-- backwards compatibility -->
<a id="schemaprojectcompact"></a>
<a id="schema_ProjectCompact"></a>
<a id="tocSprojectcompact"></a>
<a id="tocsprojectcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "project",
  "name": "Stuff to buy"
}

```

A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|

<hr>

<h2 id="tocS_ProjectMembership">ProjectMembership</h2>
<!-- backwards compatibility -->
<a id="schemaprojectmembership"></a>
<a id="schema_ProjectMembership"></a>
<a id="tocSprojectmembership"></a>
<a id="tocsprojectmembership"></a>

```json
{
  "gid": "12345",
  "resource_type": "project_membership",
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "project": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy"
  },
  "write_access": "full_write"
}

```

With the introduction of “comment-only” projects in Asana, a user’s membership in a project comes with associated permissions. These permissions (whether a user has full access to the project or comment-only access) are accessible through the project memberships endpoints described here.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|user|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|project|object|false|none|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|write_access|string|false|read-only|Whether the user has full access to the project or has comment-only access.|

#### Enumerated Values

|Property|Value|
|---|---|
|write_access|full_write|
|write_access|comment_only|

<hr>

<h2 id="tocS_ProjectMembershipCompact">ProjectMembershipCompact</h2>
<!-- backwards compatibility -->
<a id="schemaprojectmembershipcompact"></a>
<a id="schema_ProjectMembershipCompact"></a>
<a id="tocSprojectmembershipcompact"></a>
<a id="tocsprojectmembershipcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "project_membership",
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  }
}

```

With the introduction of “comment-only” projects in Asana, a user’s membership in a project comes with associated permissions. These permissions (whether a user has full access to the project or comment-only access) are accessible through the project memberships endpoints described here.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|user|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|

<hr>

<h2 id="tocS_ProjectStatus">ProjectStatus</h2>
<!-- backwards compatibility -->
<a id="schemaprojectstatus"></a>
<a id="schema_ProjectStatus"></a>
<a id="tocSprojectstatus"></a>
<a id="tocsprojectstatus"></a>

```json
{
  "gid": "12345",
  "resource_type": "project_status",
  "title": "Status Update - Jun 15",
  "created_at": "2012-02-22T02:06:58.147Z",
  "created_by": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "text": "The project is moving forward according to plan...",
  "html-text": "'&lt;body&gt;The project &lt;strong&gt;is&lt;/strong&gt; moving forward according to plan...&lt;/body&gt;'",
  "color": "green"
}

```

A *project status* is an update on the progress of a particular project, and is sent out to all project followers when created. These updates include both text describing the update and a color code intended to represent the overall state of the project: "green" for projects that are on track, "yellow" for projects at risk, and "red" for projects that are behind.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|title|string|false|read-only|The title of the project status update.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|created_by|object¦null|false|read-only|The user who created this resource.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|text|string|false|read-only|The text content of the status update.|
|html-text|string|false|read-only|[Opt In](#input-output-options). The text content of the status update with formatting as HTML.|
|color|string|false|read-only|The color associated with the status update.|

#### Enumerated Values

|Property|Value|
|---|---|
|color|green|
|color|yellow|
|color|red|

<hr>

<h2 id="tocS_ProjectStatusCompact">ProjectStatusCompact</h2>
<!-- backwards compatibility -->
<a id="schemaprojectstatuscompact"></a>
<a id="schema_ProjectStatusCompact"></a>
<a id="tocSprojectstatuscompact"></a>
<a id="tocsprojectstatuscompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "project_status",
  "title": "Status Update - Jun 15"
}

```

A *project status* is an update on the progress of a particular project, and is sent out to all project followers when created. These updates include both text describing the update and a color code intended to represent the overall state of the project: "green" for projects that are on track, "yellow" for projects at risk, and "red" for projects that are behind.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|title|string|false|read-only|The title of the project status update.|

<hr>

<h2 id="tocS_Section">Section</h2>
<!-- backwards compatibility -->
<a id="schemasection"></a>
<a id="schema_Section"></a>
<a id="tocSsection"></a>
<a id="tocssection"></a>

```json
{
  "gid": "12345",
  "resource_type": "section",
  "name": "Next Actions",
  "created_at": "2012-02-22T02:06:58.147Z",
  "projects": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    }
  ]
}

```

A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the section (i.e. the text displayed as the section header).|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|projects|[object]|false|none|none|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|

<hr>

<h2 id="tocS_SectionCompact">SectionCompact</h2>
<!-- backwards compatibility -->
<a id="schemasectioncompact"></a>
<a id="schema_SectionCompact"></a>
<a id="tocSsectioncompact"></a>
<a id="tocssectioncompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "section",
  "name": "Next Actions"
}

```

A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the section (i.e. the text displayed as the section header).|

<hr>

<h2 id="tocS_Story">Story</h2>
<!-- backwards compatibility -->
<a id="schemastory"></a>
<a id="schema_Story"></a>
<a id="tocSstory"></a>
<a id="tocsstory"></a>

```json
{
  "gid": "12345",
  "resource_type": "story",
  "resource_subtype": "milestone",
  "created_at": "2012-02-22T02:06:58.147Z",
  "created_by": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "text": "marked today",
  "type": "comment",
  "html_text": "Get whatever Sashimi has.",
  "is_edited": false,
  "is_pinned": false,
  "hearted": false,
  "hearts": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ],
  "num_hearts": 5,
  "liked": false,
  "likes": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez",
      "email": "gsanchez@example.com",
      "photo": {
        ...
      },
      "workspaces": [
        ...
      ]
    }
  ],
  "num_likes": 5,
  "previews": [
    {
      "fallback": "Greg: Great! I like this idea.\\n\\nhttps//a_company.slack.com/archives/ABCDEFG/12345678",
      "footer": "Mar 17, 2019 1:25 PM",
      "header": "Asana for Slack",
      "header_link": "https://asana.comn/apps/slack",
      "html_text": "<body>Great! I like this idea.</body>",
      "text": "Great! I like this idea.",
      "title": "Greg",
      "title_link": "https://asana.slack.com/archives/ABCDEFG/12345678"
    }
  ],
  "old_name": "This was the Old Name",
  "new_name": "This is the New Name",
  "old_dates": {
    "start_on": "2019-09-15",
    "due_at": "2012-02-22T02:06:58.158Z",
    "due_on": "2019-09-15"
  },
  "new_dates": {
    "start_on": "2019-09-15",
    "due_at": "2012-02-22T02:06:58.158Z",
    "due_on": "2019-09-15"
  },
  "old_resource_subtype": "default_task",
  "new_resource_subtype": "milestone",
  "story": {
    "gid": "12345",
    "resource_type": "story",
    "resource_subtype": "milestone",
    "created_at": "2012-02-22T02:06:58.147Z",
    "created_by": {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    },
    "text": "marked today",
    "type": "comment"
  },
  "assignee": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "follower": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "old_section": {
    "gid": "12345",
    "resource_type": "section",
    "name": "Next Actions"
  },
  "new_section": {
    "gid": "12345",
    "resource_type": "section",
    "name": "Next Actions"
  },
  "task": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task"
  },
  "project": {
    "gid": "12345",
    "resource_type": "project",
    "name": "Stuff to buy"
  },
  "tag": {
    "gid": "12345",
    "resource_type": "tag",
    "name": "Stuff to buy"
  },
  "custom_field": {
    "gid": "12345",
    "resource_type": "custom_field",
    "name": "Bug Task",
    "resource_subtype": "milestone",
    "type": "text",
    "enum_options": [
      {
        ...
      }
    ],
    "enum_value": null,
    "enabled": true,
    "text_value": "Some Value"
  },
  "old_text_value": "This was the Old Text",
  "new_text_value": "This is the New Text",
  "old_number_value": 1,
  "new_number_value": 2,
  "old_enum_value": {
    "gid": "12345",
    "resource_type": "enum_option",
    "name": "Low",
    "enabled": true,
    "color": "blue"
  },
  "new_enum_value": {
    "gid": "12345",
    "resource_type": "enum_option",
    "name": "Low",
    "enabled": true,
    "color": "blue"
  },
  "duplicate_of": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task"
  },
  "duplicated_from": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task"
  },
  "dependency": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task"
  },
  "source": "web",
  "target": {
    "gid": "1234",
    "name": "Bug Task"
  }
}

```

A story represents an activity associated with an object in the Asana system.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|created_by|object¦null|false|read-only|The user who created this resource.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|text|any|false|none|*Create-only*. Human-readable text for the story or comment.<br>This will not include the name of the creator.<br>*Note: This is not guaranteed to be stable for a given type of story. For example, text for a reassignment may not always say “assigned to …” as the text for a story can both be edited and change based on the language settings of the user making the request.*<br>Use the `resource_subtype` property to discover the action that created the story.|
|type|string|false|read-only|*Deprecated: new integrations should prefer the `resource_subtype` field.*|
|html_text|string|false|none|[Opt In](#input-output-options).<br>HTML formatted text for a comment. This will not include the name<br>of the creator.<br><br>*Note: This field is under active migration—please see our blog<br>post for more information.*|
|is_edited|boolean|false|read-only|*Conditional*. Whether the text of the story has been edited after creation.|
|is_pinned|boolean|false|none|*Conditional*. Whether the story should be pinned on the resource.|
|hearted|boolean|false|read-only|*Deprecated - please use likes instead*<br><br>*Conditional*. True if the story is hearted by the authorized user, false if not.|
|hearts|[object]|false|read-only|*Deprecated - please use likes instead*<br><br>*Conditional*. Array of users who have hearted this story.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|» email|string(email)|false|read-only|The user’s email address.|
|» photo|object¦null|false|read-only|A map of the user’s profile photo in various sizes, or null if no photo is set. Sizes provided are 21, 27, 36, 60, and 128. Images are in PNG format.|
|»» image_21x21|string(uri)|false|none|none|
|»» image_27x27|string(uri)|false|none|none|
|»» image_36x36|string(uri)|false|none|none|
|»» image_60x60|string(uri)|false|none|none|
|»» image_128x128|string(uri)|false|none|none|
|» workspaces|[object]|false|read-only|Workspaces and organizations this user may access.<br>Note\: The API will only return workspaces and organizations that also contain the authenticated user.|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|The name of the object.|
|»» email_domains|[string]|false|none|The email domains that are associated with this workspace.|
|»» is_organization|boolean|false|none|Whether the workspace is an *organization*.|
|num_hearts|integer|false|read-only|*Deprecated - please use likes instead*<br><br>*Conditional*. The number of users who have hearted this story.|
|liked|boolean|false|read-only|*Conditional*. True if the story is liked by the authorized user, false if not.|
|likes|[object]|false|read-only|*Conditional*. Array of users who have liked this story.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|» email|string(email)|false|read-only|The user’s email address.|
|» photo|object¦null|false|read-only|A map of the user’s profile photo in various sizes, or null if no photo is set. Sizes provided are 21, 27, 36, 60, and 128. Images are in PNG format.|
|»» image_21x21|string(uri)|false|none|none|
|»» image_27x27|string(uri)|false|none|none|
|»» image_36x36|string(uri)|false|none|none|
|»» image_60x60|string(uri)|false|none|none|
|»» image_128x128|string(uri)|false|none|none|
|» workspaces|[object]|false|read-only|Workspaces and organizations this user may access.<br>Note\: The API will only return workspaces and organizations that also contain the authenticated user.|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|The name of the object.|
|»» email_domains|[string]|false|none|The email domains that are associated with this workspace.|
|»» is_organization|boolean|false|none|Whether the workspace is an *organization*.|
|num_likes|integer|false|read-only|*Conditional*. The number of users who have liked this story.|
|previews|[object]|false|read-only|*Conditional*. A collection of previews to be displayed in the story.<br><br>*Note: This property only exists for comment stories.*|
|» fallback|string|false|none|Some fallback text to display if unable to display the full preview.|
|» footer|string|false|none|Text to display in the footer.|
|» header|string|false|none|Text to display in the header.|
|» header_link|string|false|none|Where the header will link to.|
|» html_text|string|false|none|HTML formatted text for the body of the preview.|
|» text|string|false|none|Text for the body of the preview.|
|» title|string|false|none|Text to display as the title.|
|» title_link|string|false|none|Where to title will link to.|
|old_name|string|false|none|*Conditional*'|
|new_name|string|false|read-only|*Conditional*|
|old_dates|object|false|read-only|*Conditional*|
|» start_on|string(date)|false|none|none|
|» due_at|string(date-time)|false|none|none|
|» due_on|string(date)|false|none|none|
|new_dates|object|false|read-only|*Conditional*|
|» start_on|string(date)|false|none|none|
|» due_at|string(date-time)|false|none|none|
|» due_on|string(date)|false|none|none|
|old_resource_subtype|string|false|read-only|*Conditional*|
|new_resource_subtype|string|false|read-only|*Conditional*|
|story|object|false|none|A story represents an activity associated with an object in the Asana system.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|» created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|» created_by|object¦null|false|read-only|The user who created this resource.|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|» text|any|false|none|*Create-only*. Human-readable text for the story or comment.<br>This will not include the name of the creator.<br>*Note: This is not guaranteed to be stable for a given type of story. For example, text for a reassignment may not always say “assigned to …” as the text for a story can both be edited and change based on the language settings of the user making the request.*<br>Use the `resource_subtype` property to discover the action that created the story.|
|» type|string|false|read-only|*Deprecated: new integrations should prefer the `resource_subtype` field.*|
|assignee|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|follower|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|old_section|object|false|none|A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the section (i.e. the text displayed as the section header).|
|new_section|object|false|none|A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the section (i.e. the text displayed as the section header).|
|task|object|false|none|The *task* is the basic object around which many operations in Asana are centered.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|project|object|false|none|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|tag|object|false|none|A *tag* is a label that can be attached to any task in Asana. It exists in a single workspace or organization.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|custom_field|object|false|none|Custom Fields store the metadata that is used in order to add user-specified information to tasks in Asana. Be sure to reference the [Custom Fields](#asana-custom-fields) developer documentation for more information about how custom fields relate to various resources in Asana.<br><br>Users in Asana can [lock custom fields](https://asana.com/guide/help/premium/custom-fields#gl-lock-fields), which will make them read-only when accessed by other users. Attempting to edit a locked custom field will return HTTP error code `403 Forbidden`.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|» resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|» type|string|false|none|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|» enum_options|[object]|false|none|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|The name of the enum option.|
|»» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|»» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|» enum_value|any|false|none|none|
|» enabled|boolean|false|none|*Conditional*. Determines if the custom field is enabled or not.|
|» text_value|string|false|none|*Conditional*. This string is the value of a text custom field.|
|old_text_value|string|false|read-only|*Conditional*|
|new_text_value|string|false|read-only|*Conditional*|
|old_number_value|integer|false|read-only|*Conditional*|
|new_number_value|integer|false|read-only|*Conditional*|
|old_enum_value|object|false|none|Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.<br><br>You can add enum options to a custom field by using the `POST /custom_fields/custom_field_gid/enum_options` endpoint.<br><br>**It is not possible to remove or delete an enum option**. Instead, enum options can be disabled by updating the `enabled` field to false with the `PUT /enum_options/enum_option_gid` endpoint. Other attributes can be updated similarly.<br><br>On creation of an enum option, `enabled` is always set to `true`, meaning the enum option is a selectable value for the custom field. Setting `enabled=false` is equivalent to “trashing” the enum option in the Asana web app within the “Edit Fields” dialog. The enum option will no longer be selectable but, if the enum option value was previously set within a task, the task will retain the value.<br><br>Enum options are an ordered list and by default new enum options are inserted at the end. Ordering in relation to existing enum options can be specified on creation by using `insert_before` or `insert_after` to reference an existing enum option. Only one of `insert_before` and `insert_after` can be provided when creating a new enum option.<br><br>An enum options list can be reordered with the `POST /custom_fields/custom_field_gid/enum_options/insert` endpoint.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the enum option.|
|» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|new_enum_value|object|false|none|Enum options are the possible values which an enum custom field can adopt. An enum custom field must contain at least 1 enum option but no more than 50.<br><br>You can add enum options to a custom field by using the `POST /custom_fields/custom_field_gid/enum_options` endpoint.<br><br>**It is not possible to remove or delete an enum option**. Instead, enum options can be disabled by updating the `enabled` field to false with the `PUT /enum_options/enum_option_gid` endpoint. Other attributes can be updated similarly.<br><br>On creation of an enum option, `enabled` is always set to `true`, meaning the enum option is a selectable value for the custom field. Setting `enabled=false` is equivalent to “trashing” the enum option in the Asana web app within the “Edit Fields” dialog. The enum option will no longer be selectable but, if the enum option value was previously set within a task, the task will retain the value.<br><br>Enum options are an ordered list and by default new enum options are inserted at the end. Ordering in relation to existing enum options can be specified on creation by using `insert_before` or `insert_after` to reference an existing enum option. Only one of `insert_before` and `insert_after` can be provided when creating a new enum option.<br><br>An enum options list can be reordered with the `POST /custom_fields/custom_field_gid/enum_options/insert` endpoint.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the enum option.|
|» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|duplicate_of|object|false|none|The *task* is the basic object around which many operations in Asana are centered.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|duplicated_from|object|false|none|The *task* is the basic object around which many operations in Asana are centered.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|dependency|object|false|none|The *task* is the basic object around which many operations in Asana are centered.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|source|string|false|read-only|The component of the Asana product the user used to trigger the story.|
|target|object|false|read-only|The object this story is associated with. Currently may only be a task.|
|» gid|string|false|none|none|
|» name|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|type|text|
|type|enum|
|type|number|

<hr>

<h2 id="tocS_StoryCompact">StoryCompact</h2>
<!-- backwards compatibility -->
<a id="schemastorycompact"></a>
<a id="schema_StoryCompact"></a>
<a id="tocSstorycompact"></a>
<a id="tocsstorycompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "story",
  "resource_subtype": "milestone",
  "created_at": "2012-02-22T02:06:58.147Z",
  "created_by": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "text": "marked today",
  "type": "comment"
}

```

A story represents an activity associated with an object in the Asana system.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|created_by|object¦null|false|read-only|The user who created this resource.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|text|any|false|none|*Create-only*. Human-readable text for the story or comment.<br>This will not include the name of the creator.<br>*Note: This is not guaranteed to be stable for a given type of story. For example, text for a reassignment may not always say “assigned to …” as the text for a story can both be edited and change based on the language settings of the user making the request.*<br>Use the `resource_subtype` property to discover the action that created the story.|
|type|string|false|read-only|*Deprecated: new integrations should prefer the `resource_subtype` field.*|

<hr>

<h2 id="tocS_Tag">Tag</h2>
<!-- backwards compatibility -->
<a id="schematag"></a>
<a id="schema_Tag"></a>
<a id="tocStag"></a>
<a id="tocstag"></a>

```json
{
  "gid": "12345",
  "resource_type": "tag",
  "name": "Stuff to buy",
  "followers": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    }
  ],
  "color": "light-green",
  "workspace": {
    "gid": "12345",
    "resource_type": "workspace",
    "name": "Bug Task"
  }
}

```

A *tag* is a label that can be attached to any task in Asana. It exists in a single workspace or organization.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|followers|[object]|false|read-only|Array of users following this tag.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|color|string|false|none|Color of the tag.|
|workspace|object|false|none|A *workspace* is the highest-level organizational unit in Asana. All projects and tasks have an associated workspace.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|

#### Enumerated Values

|Property|Value|
|---|---|
|color|dark-pink|
|color|dark-green|
|color|dark-blue|
|color|dark-red|
|color|dark-teal|
|color|dark-brown|
|color|dark-orange|
|color|dark-purple|
|color|dark-warm-gray|
|color|light-pink|
|color|light-green|
|color|light-blue|
|color|light-red|
|color|light-teal|
|color|light-brown|
|color|light-orange|
|color|light-purple|
|color|light-warm-gray|

<hr>

<h2 id="tocS_TagCompact">TagCompact</h2>
<!-- backwards compatibility -->
<a id="schematagcompact"></a>
<a id="schema_TagCompact"></a>
<a id="tocStagcompact"></a>
<a id="tocstagcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "tag",
  "name": "Stuff to buy"
}

```

A *tag* is a label that can be attached to any task in Asana. It exists in a single workspace or organization.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|

<hr>

<h2 id="tocS_Task">Task</h2>
<!-- backwards compatibility -->
<a id="schematask"></a>
<a id="schema_Task"></a>
<a id="tocStask"></a>
<a id="tocstask"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "name": "Buy catnip",
  "created_at": "2012-02-22T02:06:58.147Z",
  "resource_subtype": "default_task",
  "assignee": null,
  "assignee_status": "upcoming",
  "completed": false,
  "completed_at": "2012-02-22T02:06:58.147Z",
  "custom_fields": [
    {
      "gid": "12345",
      "resource_type": "custom_field",
      "name": "Bug Task",
      "resource_subtype": "milestone",
      "type": "text",
      "enum_options": [
        ...
      ],
      "enum_value": null,
      "enabled": true,
      "text_value": "Some Value",
      "description": "Development team priority",
      "precision": 2,
      "is_global_to_workspace": true,
      "has_notifications_enabled": true
    }
  ],
  "dependencies": [
    {
      "gid": "1234"
    },
    {
      "gid": "4321"
    }
  ],
  "dependents": [
    {
      "gid": "1234"
    },
    {
      "gid": "4321"
    }
  ],
  "due_at": "2012-02-22T02:06:58.147Z",
  "due_on": "2012-03-26",
  "external": {
    "gid": "my_gid",
    "data": "A blob of information"
  },
  "followers": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    }
  ],
  "html_notes": "<body>Mittens <em>really</em> likes the stuff from Humboldt.</body>",
  "hearted": true,
  "hearts": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    }
  ],
  "is_rendered_as_separator": false,
  "liked": true,
  "likes": [
    {
      "gid": "12345",
      "resource_type": "user",
      "name": "Greg Sanchez"
    }
  ],
  "memberships": [
    {
      "project": {
        ...
      },
      "section": {
        ...
      }
    }
  ],
  "modified_at": "2012-02-22T02:06:58.147Z",
  "notes": "Mittens really likes the stuff from Humboldt.",
  "num_hearts": 5,
  "num_likes": 5,
  "num_subtasks": 3,
  "parent": null,
  "projects": [
    {
      "gid": "12345",
      "resource_type": "project",
      "name": "Stuff to buy"
    }
  ],
  "start_on": "2012-03-26",
  "tags": [
    {
      "gid": "59746",
      "name": "Grade A"
    }
  ],
  "workspace": null
}

```

The *task* is the basic object around which many operations in Asana are centered.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|Name of the task. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.<br>The resource_subtype `milestone` represent a single moment in time. This means tasks with this subtype cannot have a start_date.<br>*Note: The resource_subtype of `section` is under active migration—please see our [forum post](https://forum.asana.com/t/sections-are-dead-long-live-sections) for more information.*|
|assignee|any|false|none|none|
|assignee_status|string|false|none|Scheduling status of this task for the user it is assigned to. This field can only be set if the assignee is non-null.|
|completed|boolean|false|none|True if the task is currently marked complete, false if not.|
|completed_at|string(date-time)¦null|false|read-only|The time at which this task was completed, or null if the task is incomplete.|
|custom_fields|[object]|false|read-only|Array of custom field values applied to the project. These represent the custom field values recorded on this project for a particular custom field. For example, these custom field values will contain an `enum_value` property for custom fields of type `enum`, a `string_value` property for custom fields of type `string`, and so on. Please note that the `gid` returned on each custom field value *is identical* to the `gid` of the custom field, which allows referencing the custom field metadata through the `/custom_fields/custom_field-gid` endpoint.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|» resource_subtype|string|false|read-only|The subtype of this resource. Different subtypes retain many of the same fields and behavior, but may render differently in Asana or represent resources with different semantic meaning.|
|» type|string|false|none|*Deprecated: new integrations should prefer the resource_subtype field.* The type of the custom field. Must be one of the given values.|
|» enum_options|[object]|false|none|*Conditional*. Only relevant for custom fields of type `enum`. This array specifies the possible values which an `enum` custom field can adopt. To modify the enum options, refer to [working with enum options](#create-an-enum-option).|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|The name of the enum option.|
|»» enabled|boolean|false|none|The color of the enum option. Defaults to ‘none’.|
|»» color|string|false|none|Whether or not the enum option is a selectable value for the custom field.|
|» enum_value|any|false|none|none|
|» enabled|boolean|false|none|*Conditional*. Determines if the custom field is enabled or not.|
|» text_value|string|false|none|*Conditional*. This string is the value of a text custom field.|
|» description|string|false|none|[Opt In](#input-output-options). The description of the custom field.|
|» precision|integer|false|none|Only relevant for custom fields of type ‘Number’. This field dictates the number of places after the decimal to round to, i.e. 0 is integer values, 1 rounds to the nearest tenth, and so on. Must be between 0 and 6, inclusive.|
|» is_global_to_workspace|boolean|false|read-only|This flag describes whether this custom field is available to every container in the workspace. Before project-specific custom fields, this field was always true.|
|» has_notifications_enabled|boolean|false|none|This flag describes whether a follower of a task with this field should receive inbox notifications from changes to this field.|
|dependencies|[object]|false|read-only|[Opt In](#input-output-options). Array of resources referencing tasks that this task depends on. The objects contain only the gid of the dependency.|
|» gid|string|false|none|none|
|dependents|[object]|false|read-only|[Opt In](#input-output-options). Array of resources referencing tasks that depend on this task. The objects contain only the ID of the dependent.|
|» gid|string|false|none|none|
|due_at|string(date)¦null|false|none|Date and time on which this task is due, or null if the task has no due time. This takes a UTC timestamp and should not be used together with `due_on`.|
|due_on|string(date)¦null|false|none|Date on which this task is due, or null if the task has no due date.  This takes a date with `YYYY-MM-DD` format and should not be used together with due_at.|
|external|object|false|none|*OAuth Required*. *Conditional*. This field is returned only if external values are set or included by using [Opt In] (#input-output-options).<br>The external field allows you to store app-specific metadata on tasks, including a gid that can be used to retrieve tasks and a data blob that can store app-specific character strings. Note that you will need to authenticate with Oauth to access or modify this data. Once an external gid is set, you can use the notation `external:custom_gid` to reference your object anywhere in the API where you may use the original object gid. See the page on Custom External Data for more details.|
|» gid|string|false|none|none|
|» data|string|false|none|none|
|followers|[object]|false|read-only|Array of users following this task.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|html_notes|string|false|none|[Opt In](#input-output-options). The notes of the text with formatting as HTML.<br>*Note: This field is under active migration—please see our blog post for more information.*|
|hearted|boolean|false|read-only|*Deprecated - please use liked instead* True if the task is hearted by the authorized user, false if not.|
|hearts|[object]|false|read-only|*Deprecated - please use likes instead* Array of users who have hearted this task.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|is_rendered_as_separator|boolean|false|read-only|[Opt In](#input-output-options). In some contexts tasks can be rendered as a visual separator; for instance, subtasks can appear similar to [sections](#asana-sections) without being true `section` objects. If a `task` object is rendered this way in any context it will have the property `is_rendered_as_separator` set to `true`.<br /><br />*Note: Until the default behavior for our API changes integrations must [opt in to the `new_sections` change] (https://forum.asana.com/t/sections-are-dead-long-live-sections/33951) to modify the `is_rendered_as_separator` property.*|
|liked|boolean|false|read-only|True if the task is liked by the authorized user, false if not.|
|likes|[object]|false|read-only|Array of users who have liked this task.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|memberships|[object]|false|read-only|*Create-only*. Array of projects this task is associated with and the section it is in. At task creation time, this array can be used to add the task to specific sections. After task creation, these associations can be modified using the `addProject` and `removeProject` endpoints. Note that over time, more types of memberships may be added to this property.|
|» project|object|false|none|A *project* represents a prioritized list of tasks in Asana or a board with columns of tasks represented as cards. It exists in a single workspace or organization and is accessible to a subset of users in that workspace or organization, depending on its permissions.|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|» section|object|false|none|A *section* is a subdivision of a project that groups tasks together. It can either be a header above a list of tasks in a list view or a column in a board view of a project.|
|»» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|»» resource_type|string|false|read-only|The base type of this resource.|
|»» name|string|false|none|The name of the section (i.e. the text displayed as the section header).|
|modified_at|string(date-time)|false|read-only|The time at which this task was last modified.<br><br>*Note: This does not currently reflect any changes in<br>associations such as projects or comments that may have been<br>added or removed from the task.*|
|notes|string|false|none|More detailed, free-form textual information associated with the task.|
|num_hearts|integer|false|read-only|*Deprecated - please use likes instead* The number of users who have hearted this task.|
|num_likes|integer|false|read-only|The number of users who have liked this task.|
|num_subtasks|integer|false|read-only|[Opt In](#input-output-options). The number of subtasks on this task.|
|parent|any|false|none|none|
|projects|[object]|false|read-only|*Create-only.* Array of projects this task is associated with. At task creation time, this array can be used to add the task to many projects at once. After task creation, these associations can be modified using the addProject and removeProject endpoints.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the project. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|start_on|string(date)¦null|false|none|The day on which work begins for the task , or null if the task has no start date. This takes a date with `YYYY-MM-DD` format.<br>*Note: `due_on` or `due_at` must be present in the request when setting or unsetting the `start_on` parameter.*|
|tags|[object]|false|read-only|*Create-only*. Array of tags associated with this task. This property may be specified on creation using just an array of tag gids.  In order to change tags on an existing task use `addTag` and `removeTag`.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|Name of the tag. This is generally a short sentence fragment that fits on a line in the UI for maximum readability. However, it can be longer.|
|workspace|any|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|resource_subtype|default_task|
|resource_subtype|milestone|
|resource_subtype|section|
|assignee_status|today|
|assignee_status|upcoming|
|assignee_status|later|
|assignee_status|new|
|assignee_status|inbox|
|type|text|
|type|enum|
|type|number|

<hr>

<h2 id="tocS_TaskCompact">TaskCompact</h2>
<!-- backwards compatibility -->
<a id="schemataskcompact"></a>
<a id="schema_TaskCompact"></a>
<a id="tocStaskcompact"></a>
<a id="tocstaskcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "name": "Bug Task"
}

```

The *task* is the basic object around which many operations in Asana are centered.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|

<hr>

<h2 id="tocS_Team">Team</h2>
<!-- backwards compatibility -->
<a id="schemateam"></a>
<a id="schema_Team"></a>
<a id="tocSteam"></a>
<a id="tocsteam"></a>

```json
{
  "gid": "12345",
  "resource_type": "team",
  "name": "Bug Task",
  "description": "All developers should be members of this team.",
  "html_description": "<body><em>All</em> developers should be members of this team.</body>",
  "organization": null
}

```

A *team* is used to group related projects and people together within an organization. Each project in an organization is associated with a team.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|
|description|string|false|none|[Opt In](#input-output-options). The description of the team.|
|html_description|string|false|none|[Opt In](#input-output-options). The description of the team with formatting as HTML.<br>*Note: This field is under active migration—please see our [blog post](https://developers.asana.com/docs/#rich-text) for more information.*|
|organization|any|false|none|none|

<hr>

<h2 id="tocS_TeamCompact">TeamCompact</h2>
<!-- backwards compatibility -->
<a id="schemateamcompact"></a>
<a id="schema_TeamCompact"></a>
<a id="tocSteamcompact"></a>
<a id="tocsteamcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "team",
  "name": "Bug Task"
}

```

A *team* is used to group related projects and people together within an organization. Each project in an organization is associated with a team.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|

<hr>

<h2 id="tocS_User">User</h2>
<!-- backwards compatibility -->
<a id="schemauser"></a>
<a id="schema_User"></a>
<a id="tocSuser"></a>
<a id="tocsuser"></a>

```json
{
  "gid": "12345",
  "resource_type": "user",
  "name": "Greg Sanchez",
  "email": "gsanchez@example.com",
  "photo": {
    "image_21x21": "https://...",
    "image_27x27": "https://...",
    "image_36x36": "https://...",
    "image_60x60": "https://...",
    "image_128x128": "https://..."
  },
  "workspaces": [
    {
      "gid": "12345",
      "resource_type": "task",
      "name": "Bug Task",
      "email_domains": [
        ...
      ],
      "is_organization": false
    }
  ]
}

```

A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|email|string(email)|false|read-only|The user’s email address.|
|photo|object¦null|false|read-only|A map of the user’s profile photo in various sizes, or null if no photo is set. Sizes provided are 21, 27, 36, 60, and 128. Images are in PNG format.|
|» image_21x21|string(uri)|false|none|none|
|» image_27x27|string(uri)|false|none|none|
|» image_36x36|string(uri)|false|none|none|
|» image_60x60|string(uri)|false|none|none|
|» image_128x128|string(uri)|false|none|none|
|workspaces|[object]|false|read-only|Workspaces and organizations this user may access.<br>Note\: The API will only return workspaces and organizations that also contain the authenticated user.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|» email_domains|[string]|false|none|The email domains that are associated with this workspace.|
|» is_organization|boolean|false|none|Whether the workspace is an *organization*.|

<hr>

<h2 id="tocS_UserCompact">UserCompact</h2>
<!-- backwards compatibility -->
<a id="schemausercompact"></a>
<a id="schema_UserCompact"></a>
<a id="tocSusercompact"></a>
<a id="tocsusercompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "user",
  "name": "Greg Sanchez"
}

```

A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|*Read-only except when same user as requester*. The user’s name.|

<hr>

<h2 id="tocS_UserTaskList">UserTaskList</h2>
<!-- backwards compatibility -->
<a id="schemausertasklist"></a>
<a id="schema_UserTaskList"></a>
<a id="tocSusertasklist"></a>
<a id="tocsusertasklist"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "name": "Bug Task",
  "owner": null,
  "workspace": null
}

```

A user task list represents the tasks assigned to a particular user. It provides API access to a user’s “My Tasks” view in Asana.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|
|owner|any|false|none|none|
|workspace|any|false|none|none|

<hr>

<h2 id="tocS_UserTaskListCompact">UserTaskListCompact</h2>
<!-- backwards compatibility -->
<a id="schemausertasklistcompact"></a>
<a id="schema_UserTaskListCompact"></a>
<a id="tocSusertasklistcompact"></a>
<a id="tocsusertasklistcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "name": "Bug Task"
}

```

A generic Asana Object, containing a globally unique identifier.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|

<hr>

<h2 id="tocS_Webhook">Webhook</h2>
<!-- backwards compatibility -->
<a id="schemawebhook"></a>
<a id="schema_Webhook"></a>
<a id="tocSwebhook"></a>
<a id="tocswebhook"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "created_at": "2012-02-22T02:06:58.147Z",
  "active": false,
  "last_failure_at": "2012-02-22T02:06:58.147Z",
  "last_failure_content": "500 Server Error\\n\\nCould not complete the request",
  "last_success_at": "2012-02-22T02:06:58.147Z",
  "resource": null,
  "target": "https://example.com/receive-webhook/7654"
}

```

Webhooks allow an application to be notified of changes. This is in addition to the ability to fetch those changes directly as Events - in fact, Webhooks are just a way to receive [Events](#asana-events) via HTTP POST at the time they occur instead of polling for them. For services accessible via HTTP this is often vastly more convenient, and if events are not too frequent can be significantly more efficient.

In both cases, however, changes are represented as Event objects - refer to the [Events documentation](#asana-events) for more information on what data these events contain.

*Note: While Webhooks send arrays of Event objects to their target, the Event objects themselves contain *only gids*, rather than the actual resource they are referencing. Webhooks themselves contain only the information necessary to deliver the events to the desired target as they are generated.*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|created_at|string(date-time)|false|read-only|The time at which this resource was created.|
|active|boolean|false|none|If true, the webhook will send events - if false it is considered inactive and will not generate events.|
|last_failure_at|string(date-time)|false|read-only|The timestamp when the webhook last received an error when sending an event to the target.|
|last_failure_content|string|false|read-only|The contents of the last error response sent to the webhook when attempting to deliver events to the target.|
|last_success_at|string(date-time)|false|read-only|The timestamp when the webhook last successfully sent an event to the target.|
|resource|any|false|none|none|
|target|string(uri)|false|read-only|The URL to receive the HTTP POST.|

<hr>

<h2 id="tocS_WebhookEvent">WebhookEvent</h2>
<!-- backwards compatibility -->
<a id="schemawebhookevent"></a>
<a id="schema_WebhookEvent"></a>
<a id="tocSwebhookevent"></a>
<a id="tocswebhookevent"></a>

```json
{
  "action": "changed",
  "created_at": "2012-02-22T02:06:58.147Z",
  "parent": "12345",
  "resource": "32154",
  "type": "task",
  "user": "321654987"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|action|string|false|read-only|The type of action taken that triggered the event.|
|created_at|string(date-time)|false|read-only|The timestamp when the event occurred.|
|parent|string¦null|false|read-only|For added/removed events, the parent gid that resource was added to or removed from. The parent will be `null` for other event types.|
|resource|string|false|read-only|The resource gid the event occurred on.<br><br>*Note: The resource that triggered the event may be different from<br>the one that the events were requested for. For example, a<br>subscription to a project will contain events for tasks contained<br>within the project.*|
|type|string|false|read-only|The type of the resource that generated the event.<br><br>*Note: Currently, only tasks, projects and stories generate<br>events.*|
|user|string¦null|false|read-only|The gid of the user who triggered the event.<br><br>*Note: The event may be triggered by a different user than the<br>subscriber. For example, if user A subscribes to a task and user B<br>modified it, the event’s user will be user B. Note: Some events are<br>generated by the system, and will have `null` as the user. API<br>consumers should make sure to handle this case.*|

<hr>

<h2 id="tocS_Workspace">Workspace</h2>
<!-- backwards compatibility -->
<a id="schemaworkspace"></a>
<a id="schema_Workspace"></a>
<a id="tocSworkspace"></a>
<a id="tocsworkspace"></a>

```json
{
  "gid": "12345",
  "resource_type": "task",
  "name": "Bug Task",
  "email_domains": [
    "asana.com"
  ],
  "is_organization": false
}

```

A generic Asana Object, containing a globally unique identifier.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|
|email_domains|[string]|false|none|The email domains that are associated with this workspace.|
|is_organization|boolean|false|none|Whether the workspace is an *organization*.|

<hr>

<h2 id="tocS_WorkspaceCompact">WorkspaceCompact</h2>
<!-- backwards compatibility -->
<a id="schemaworkspacecompact"></a>
<a id="schema_WorkspaceCompact"></a>
<a id="tocSworkspacecompact"></a>
<a id="tocsworkspacecompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "workspace",
  "name": "Bug Task"
}

```

A *workspace* is the highest-level organizational unit in Asana. All projects and tasks have an associated workspace.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The base type of this resource.|
|name|string|false|none|The name of the object.|

<hr>

<h2 id="tocS_WorkspaceMembership">WorkspaceMembership</h2>
<!-- backwards compatibility -->
<a id="schemaworkspacemembership"></a>
<a id="schema_WorkspaceMembership"></a>
<a id="tocSworkspacemembership"></a>
<a id="tocsworkspacemembership"></a>

```json
{
  "gid": "12345",
  "resource_type": "workspace_membership",
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "workspace": {
    "gid": "12345",
    "resource_type": "workspace",
    "name": "Bug Task"
  },
  "user_task_list": {
    "gid": "12345",
    "resource_type": "task",
    "name": "Bug Task",
    "owner": null,
    "workspace": null
  },
  "is_active": true,
  "is_admin": true,
  "is_guest": true
}

```

This object determines if a user is a member of a workspace.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The resource type of this resource. The value for this resource is always `workspace_membership`.|
|user|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|workspace|object|false|none|A *workspace* is the highest-level organizational unit in Asana. All projects and tasks have an associated workspace.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|user_task_list|object|false|none|A user task list represents the tasks assigned to a particular user. It provides API access to a user’s “My Tasks” view in Asana.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|
|» owner|any|false|none|none|
|» workspace|any|false|none|none|
|is_active|boolean|false|read-only|Reflects if this user still a member of the workspace.|
|is_admin|boolean|false|read-only|Reflects if this user is an admin of the workspace.|
|is_guest|boolean|false|read-only|Reflects if this user is a guest of the workspace.|

<hr>

<h2 id="tocS_WorkspaceMembershipCompact">WorkspaceMembershipCompact</h2>
<!-- backwards compatibility -->
<a id="schemaworkspacemembershipcompact"></a>
<a id="schema_WorkspaceMembershipCompact"></a>
<a id="tocSworkspacemembershipcompact"></a>
<a id="tocsworkspacemembershipcompact"></a>

```json
{
  "gid": "12345",
  "resource_type": "workspace_membership",
  "user": {
    "gid": "12345",
    "resource_type": "user",
    "name": "Greg Sanchez"
  },
  "workspace": {
    "gid": "12345",
    "resource_type": "workspace",
    "name": "Bug Task"
  }
}

```

This object determines if a user is a member of a workspace.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|resource_type|string|false|read-only|The resource type of this resource. The value for this resource is always `workspace_membership`.|
|user|object|false|none|A *user* object represents an account in Asana that can be given access to various workspaces, projects, and tasks.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|*Read-only except when same user as requester*. The user’s name.|
|workspace|object|false|none|A *workspace* is the highest-level organizational unit in Asana. All projects and tasks have an associated workspace.|
|» gid|string|false|read-only|Globally unique identifier of the object, as a string.|
|» resource_type|string|false|read-only|The base type of this resource.|
|» name|string|false|none|The name of the object.|

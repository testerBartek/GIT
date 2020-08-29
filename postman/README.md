# Postman

{% embed url="https://learning.postman.com/docs/getting-started/introduction/" caption="Postman Documentation" %}

{% embed url="https://www.guru99.com/postman-tutorial.html" caption="Basic of Postman and Newman" %}

{% page-ref page="newman.md" %}

## Request

![](../.gitbook/assets/image%20%2811%29.png)

### Query Params

?KEY=VALUE

### Path Variables

:userid  


## Scripts and tests

| **Basic test structure** |
| :--- |
| pm.test\("Status code is 200", function \(\) {      pm.response.to.have.status\(200\);  }\); |

| Response assertions |
| :--- |
| pm.response.to.have.status\(200\); |
| pm.expect\(pm.response.responseTime\).to.be.below\(200\); |
| pm.response.to.have.header\(”X-Cache"\); |
| pm.response.to.have.header\(”X-Cache", “HIT”\); |
| pm.expect\(pm.cookies.has\("sessionId"\)\).to.be.true; |
| pm.expect\(pm.cookies.get\("sessionId"\)\).to.equal\("abcb9s"\); |
| pm.response.to.have.body\( "OK"\); |
| pm.expect\(pm.response.text\(\)\).to.include\("Order placed."\); |

| Variables |
| :--- |
| pm.globals.set\("varName", "VALUE"\); |
| pm.globals.get\("varName"\); |
| pm.globals.unset\("varName"\); |
| pm.globals.clear\(\); |
| pm.environment.set\("varName", "VALUE"\); |
| pm.environment.get\("varName"\); |
| pm.environment.unset\("varName"\); |
| pm.environment.clear\(\) |
| pm.variables.get\("varName"\) |

## Learn Postman by Trello API

{% embed url="https://developer.atlassian.com/cloud/trello/" caption="Start with trello API" %}

{% embed url="https://developer.atlassian.com/cloud/trello/rest/api-group-actions/" caption="REST API lists" %}

### Postman Trello API requests and tests:

1. Create a trello board
2. Create two lists TODO and DONE
3. Create a new card inside TODO
4. Move the card to DONE
5. Delete the board

{% file src="../.gitbook/assets/apitrello.postman\_collection.json" caption="Collection of API Trello" %}

{% file src="../.gitbook/assets/apitrello.postman\_test\_run.json" caption="Export Results from Collection Runner" %}

## Variables

`{{ENVIRONMENT_VARIABLES}} -> Use to easy switch environment. Allways is used before Global Variables`

`{{GLOBAL_VARIABLES}} -> The same like Environment but it's not easy to switch. And Environment variables has bigger priority.`

## Debugging tests

`console.log(response.prefs);`

`and click Console to see it.`

## GitHub API



{% embed url="https://developer.github.com/v3/repos/" caption="It could be out of date" %}

{% embed url="https://docs.github.com/en/rest/reference/repos" caption="Documentation of GitHub API" %}

{% api-method method="get" host="  https://api.github.com" path="/user/repos" %}
{% api-method-summary %}
GitHub Repository
{% endapi-method-summary %}

{% api-method-description %}
1. Authorization &gt; _Type - Basic Auth &gt; Username/Password to GitHub_  
2. Send Request
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.github.com/user/repos" path=" " %}
{% api-method-summary %}
Create a new Repo
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="description" type="string" required=true %}
"This is a test repository created by Postman"
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
"Test-Repository"
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="  https://api.github.com/repos/:owner/:repo" path=" " %}
{% api-method-summary %}
 Check public Repo
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="repo" type="string" required=false %}
Test-Repository
{% endapi-method-parameter %}

{% api-method-parameter name="owner" type="string" required=true %}
testerBartek  
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.github.com/repos/:{owner}/:{repo}/issues" path=" " %}
{% api-method-summary %}
Create Issue 
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{repo}" type="string" required=true %}
Test-Repository
{% endapi-method-parameter %}

{% api-method-parameter name="{owner}" type="string" required=true %}
testerBartek
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="body" type="string" required=true %}
"This issue has been automatically created by Postman"
{% endapi-method-parameter %}

{% api-method-parameter name="title" type="string" required=true %}
"Found a bug"
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="  https://api.github.com/repos/:{owner}/:{repo}/issues/:{issue\_number}" path=" " %}
{% api-method-summary %}
 Check created Issue
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{issue\_number}" type="string" required=false %}
1
{% endapi-method-parameter %}

{% api-method-parameter name="{repo}" type="string" required=true %}
Test-Repository
{% endapi-method-parameter %}

{% api-method-parameter name="{owner}" type="string" required=true %}
testerBartek
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host=" https://api.github.com/repos/:{owner}/:{repo}" path=" " %}
{% api-method-summary %}
Delete GitHub Repo
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{repo}" type="string" required=true %}
Test-Repository
{% endapi-method-parameter %}

{% api-method-parameter name="{owner}" type="string" required=true %}
testerBartek
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host=" https://api.github.com/repos/:{owner}/:{repo}" path=" " %}
{% api-method-summary %}
Check deleted Repo
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="{repo}" type="string" required=true %}
Test-Repository
{% endapi-method-parameter %}

{% api-method-parameter name="{owner}" type="string" required=true %}
testerBartek
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Collection and test run

{% file src="../.gitbook/assets/github.postman\_test\_run.json" %}

{% file src="../.gitbook/assets/github.postman\_collection.json" caption="GitHub.postman\_collection.json" %}


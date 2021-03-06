---
description: The Easiest way to define custom resources
---

# Custom Metadata

As it was said earlier Aidbox is a metadata driven platform, therefore when you want to define new ResourceType, or Attribute you need to create a couple of resources, such as Entity and Attribute. And  sometimes this way is not convenient. For this reason we support special endpoint that provide to you more simply way to define custom Metadata.

 For example, lets try to define two custom resources: **City** and **Country**. ****Country will consists of name, population and flag**.** City consists of name, phoneCode, reference to country and date of foundation. Also we want that Country.name, City.name and City.country attributes should be required. And we are want to search Country by name and population, City by name and country  in which it is located

{% tabs %}
{% tab title="First Tab" %}
```yaml
definitions:
  Country:
    properties:
      name: {"type": "string"}
      population: {"type": "number"}
      flag: {"type": "Attachment"}
    required: ["name"]
    search:
      name:
        expression: [["name"]]
        type: "string"
      population:
        expression: [["name"]]
        type: "number"
  City:
    properties:
      name: {"type": "string"}
      phoneCode: {"type": "string"}
      country: {"type": "Reference"}
      foundation: {"type": "date"}
    required: ["name", "country"]
    search:
      name:
        expression: [["name"]]
        type: "string"
      country:
        expression: [["country"]]
        type: "reference"
```
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

{% api-method method="post" host="\[base\]" path="/$metadata" %}
{% api-method-summary %}
Metadata
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" %}
ID of the cake to get, for free of course.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Authentication token to track down who is emptying our stocks.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="recipe" type="string" %}
The API will do its best to find a cake matching the provided recipe.
{% endapi-method-parameter %}

{% api-method-parameter name="gluten" type="boolean" %}
Whether the cake should be gluten-free or not.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```yaml
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}




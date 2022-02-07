# Open api code for creating mock api through aws api-gateway to return mock json response of provided mock json data

```
{
  "openapi" : "3.0.1",
  "info" : {
    "title" : "Message api",
    "description" : "Mock API",
    "version" : "2022-01-27T15:38:14Z"
  },
  "servers" : [ {
    "url" : "https://<api-key>.execute-api.us-east-1.amazonaws.com/{basePath}",
    "variables" : {
      "basePath" : {
        "default" : "/v1"
      }
    }
  } ],
  "paths" : {
    "/message" : {
      "get" : {
        "responses" : {
          "200" : {
            "description" : "200 response",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Empty"
                }
              }
            }
          }
        },
        "x-amazon-apigateway-integration" : {
          "responses" : {
            "default" : {
              "statusCode" : "200",
              "responseTemplates" : {
                "application/json" : "{\r\n  \"comment\": \"DataTransformer JSON\",\r\n  \"genericDrugName\":\"zyloric\",\r\n  \"adverseReaction\":\"uric acid\"\r\n},\r\n{\r\n  \"comment\": \"DataTransformer JSON\",\r\n  \"genericDrugName\":\"pioz\",\r\n  \"adverseReaction\":\"diabetes\"\r\n},\r\n{\r\n  \"comment\": \"DataTransformer JSON\",\r\n  \"genericDrugName\":\"Pudinhara\",\r\n  \"adverseReaction\":\"acidity\"\r\n},\r\n{\r\n  \"comment\": \"DataTransformer JSON\",\r\n  \"genericDrugName\":\"Nerokind\",\r\n  \"adverseReaction\":\"diabetes\"\r\n},\r\n{\r\n  \"comment\": \"DataTransformer JSON\",\r\n  \"genericDrugName\":\"Giloy\",\r\n  \"adverseReaction\":\"immunity\"\r\n}"
              }
            }
          },
          "requestTemplates" : {
            "application/json" : "{\"statusCode\": 200}"
          },
          "passthroughBehavior" : "when_no_match",
          "type" : "mock"
        }
      }
    }
  },
  "components" : {
    "schemas" : {
      "Empty" : {
        "title" : "Empty Schema",
        "type" : "object"
      }
    }
  }
}
```

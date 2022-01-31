# Mock integration api through aws api-gateway to return mock json response on the basis of input string query parameter

```
{
  "openapi" : "3.0.1",
  "info" : {
    "title" : "Mock integration api",
    "description" : "Mock API",
    "version" : "2022-01-27T16:10:46Z"
  },
  "servers" : [ {
    "url" : "https://hk0ktiwzuf.execute-api.us-east-1.amazonaws.com/{basePath}",
    "variables" : {
      "basePath" : {
        "default" : "/v1"
      }
    }
  } ],
  "paths" : {
    "/message" : {
      "get" : {
        "parameters" : [ {
          "name" : "scope",
          "in" : "query",
          "schema" : {
            "type" : "string"
          }
        } ],
        "responses" : {
          "500" : {
            "description" : "500 response",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Error"
                }
              }
            }
          },
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
                "application/json" : "{\r\n    \"statusCode\": 200,\r\n    \"message\": \"Go ahead without me\"\r\n}"
              }
            },
            "5\\d{2}" : {
              "statusCode" : "500",
              "responseTemplates" : {
                "application/json" : "{\r\n    \"statusCode\": 500,\r\n    \"message\": \"The invoked method is not supported on the API resource.\"\r\n}"
              }
            }
          },
          "requestTemplates" : {
            "application/json" : "{\r\n  #if( $input.params('scope') == \"internal\" )\r\n    \"statusCode\": 200\r\n  #else\r\n    \"statusCode\": 500\r\n  #end\r\n}"
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
      },
      "Error" : {
        "title" : "Error Schema",
        "type" : "object",
        "properties" : {
          "message" : {
            "type" : "string"
          }
        }
      }
    }
  }
}
```

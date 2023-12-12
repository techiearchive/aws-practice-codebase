## Assignment1: Open api code to create sample api through aws api-gateway

```
{
  "openapi" : "3.0.1",
  "info" : {
    "title" : "assignment-1",
    "version" : "2023-01-16T14:43:20Z"
  },
  "servers" : [ {
    "url" : "https://<api-key>.execute-api.us-east-1.amazonaws.com/{basePath}",
    "variables" : {
      "basePath" : {
        "default" : "dev"
      }
    }
  } ],
  "paths" : {
    "/store-data" : {
      "post" : {
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
        }
      },
      "options" : {
        "responses" : {
          "200" : {
            "description" : "200 response",
            "headers" : {
              "Access-Control-Allow-Origin" : {
                "schema" : {
                  "type" : "string"
                }
              },
              "Access-Control-Allow-Methods" : {
                "schema" : {
                  "type" : "string"
                }
              },
              "Access-Control-Allow-Headers" : {
                "schema" : {
                  "type" : "string"
                }
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Empty"
                }
              }
            }
          }
        }
      }
    },
    "/fetch-data" : {
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
        }
      },
      "options" : {
        "responses" : {
          "200" : {
            "description" : "200 response",
            "headers" : {
              "Access-Control-Allow-Origin" : {
                "schema" : {
                  "type" : "string"
                }
              },
              "Access-Control-Allow-Methods" : {
                "schema" : {
                  "type" : "string"
                }
              },
              "Access-Control-Allow-Headers" : {
                "schema" : {
                  "type" : "string"
                }
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Empty"
                }
              }
            }
          }
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

# Open api code to create api through aws api-gateway to upload image into s3 bucket

```
{
  "openapi" : "3.0.1",
  "info" : {
    "title" : "upload-to-s3",
    "version" : "2022-01-25T14:57:23Z"
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
    "/{folder}/{object}" : {
      "put" : {
        "parameters" : [ {
          "name" : "object",
          "in" : "path",
          "required" : true,
          "schema" : {
            "type" : "string"
          }
        }, {
          "name" : "folder",
          "in" : "path",
          "required" : true,
          "schema" : {
            "type" : "string"
          }
        } ],
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
          "credentials" : "<Iam role>",
          "httpMethod" : "PUT",
          "uri" : "arn:aws:apigateway:us-east-1:s3:path/{bucket}/{key}",
          "responses" : {
            "default" : {
              "statusCode" : "200"
            }
          },
          "requestParameters" : {
            "integration.request.path.key" : "method.request.path.object",
            "integration.request.path.bucket" : "method.request.path.folder"
          },
          "passthroughBehavior" : "when_no_match",
          "type" : "aws"
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
  },
  "x-amazon-apigateway-binary-media-types" : [ "image/jpeg" ]
}
```

# Reference:
[api-gateway-upload-image-s3](https://aws.amazon.com/premiumsupport/knowledge-center/api-gateway-upload-image-s3/)

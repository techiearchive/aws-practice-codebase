# Api to upload and download binary files from S3 bucket. Eg: Image files.

```
{
  "openapi" : "3.0.1",
  "info" : {
    "title" : "access-s3-binary",
    "version" : "2022-02-07T14:57:23Z"
  },
  "paths" : {
    "/s3" : {
      "get" : {
        "parameters" : [ {
          "name" : "key",
          "in" : "query",
          "schema" : {
            "type" : "string"
          }
        } ],
        "responses" : {
          "500" : {
            "description" : "500 response",
            "content" : { }
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
          "credentials" : "<iam role>",
          "httpMethod" : "GET",
          "uri" : "arn:aws:apigateway:us-east-1:s3:path/api-gateway-files/{key}",
          "responses" : {
            "default" : {
              "statusCode" : "500",
              "responseTemplates" : {
                "application/json" : "{\r\n    \"statusCode\": 500,\r\n    \"message\": \"The invoked parameter is not supported on the API resource.\"\r\n}"
              }
            },
            "2\\d{2}" : {
              "statusCode" : "200"
            }
          },
          "requestParameters" : {
            "integration.request.path.key" : "method.request.querystring.key"
          },
          "passthroughBehavior" : "when_no_match",
          "type" : "aws"
        }
      },
      "put" : {
        "parameters" : [ {
          "name" : "key",
          "in" : "query",
          "required" : true,
          "schema" : {
            "type" : "string"
          }
        } ],
        "responses" : {
          "500" : {
            "description" : "500 response",
            "content" : { }
          },
          "200" : {
            "description" : "200 response",
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Empty"
                }
              },
              "application/octet-stream" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Empty"
                }
              }
            }
          }
        },
        "x-amazon-apigateway-integration" : {
          "credentials" : "<iam role>",
          "httpMethod" : "PUT",
          "uri" : "arn:aws:apigateway:us-east-1:s3:path/api-gateway-files/{key}",
          "responses" : {
            "default" : {
              "statusCode" : "500",
              "responseTemplates" : {
                "application/json" : "{\r\n    \"statusCode\": 500,\r\n    \"message\": \"The invoked parameter is not supported on the API resource.\"\r\n}"
              }
            },
            "2\\d{2}" : {
              "statusCode" : "200",
              "responseTemplates" : {
                "application/json" : "{\r\n    \"statusCode\": 200,\r\n    \"message\": \"File succesfully uploaded\"\r\n}"
              }
            }
          },
          "requestParameters" : {
            "integration.request.path.key" : "method.request.querystring.key"
          },
          "passthroughBehavior" : "when_no_match",
          "contentHandling" : "CONVERT_TO_BINARY",
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
  "x-amazon-apigateway-binary-media-types" : [ "application/octet-stream", "image/jpeg" ]
}
```
# Iam role policy to access the s3 bucket
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject"
            ],
            "Resource": "arn:aws:s3:::<bucket-name>/*"
        }
    ]
}
```

# Reference:
[Access binary files from S3](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-content-encodings-examples-image-s3.html)

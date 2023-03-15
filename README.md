# defectdojo findings thresholds v1

This GitHub Action that queries the number of active finding in DefectDojo by product and then compares them against the thresholds set by the user, failing the build if the thresholds are exceeded.

portswigger-cloud/defectdojo-findings-thresholds@v1

__Example output__

The total number of my-product findings 61 is greater than the configured threshold of 50

## About DefectDojo

[DefectDojo](https://github.com/DefectDojo/django-DefectDojo) is a security orchestration and vulnerability management platform. DefectDojo allows you to manage your application security program, maintain product and application information, triage vulnerabilities and push findings to systems like JIRA and Slack. DefectDojo enriches and refines vulnerability data using a number of heuristic algorithms that improve with the more you use the platform.

## Inputs

| Input Name                   | Required |
| ---------------------------- | -------- | 
| defectdojo-url               | True     |
| defectdojo-username          | True     |
| defectdojo-password          | True     |
| defectdojo-product           | True     |
| total-threshold              | False    |
| critical-threshold           | False    |
| high-threshold               | False    |
| medium-threshold             | False    |
| low-threshold                | False    |
| info-threshold               | False    |

If any of the thresholds are left blank they will not evaluated by this action.

## Examples

### Simple example

```
name: test-security-findings-threshold-by-product-against-active-findings-from-defectdojo
on:
  push
jobs:
  test-active-findings-against-thresholds:
    runs-on: ubuntu-latest
    steps:
      - name: defectdojo_findings-threshold:
        id: defectdojo-findings-threshold:
        uses: portswigger-cloud/defectdojo-active-findings@main
        with:
          defectdojo-url: https://defectdojo.example.con
          defectdojo-username: ${{ secrets.defectdojo-username }}
          defectdojo-password: ${{ secrets.defectdojo-password }}
          defectdojo-product: my-product
          total-threshold: 10
          critical-threshold: 2 
          high-threshold: 2
          medium-threshold: 2
          low-threshold: 2
          info-threshold: 2
```
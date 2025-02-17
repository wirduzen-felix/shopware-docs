# 2022-05-12 - Remove static analysis with psalm

{% hint style="info" %}
This document represents an architecture decision record (ADR) and has been mirrored from the ADR section in our Shopware 6 repository.
You can find the original version [here](https://github.com/shopware/platform/blob/trunk/resources/references/adr/workflow/2022-05-12-remove-static-analysis-with-psalm.md)
{% endhint %}

## Context
Currently, we are running static analysis over the php code with both `phpstan` and `psalm`.
This slows down our pipeline and may lead to weird effects where `phpstan` and `psalm` report errors that are incompatible with each other. 

## Decision
There is not much need anymore to run both tools, as they pretty much converged to a common feature set.
This was different when we started with shopware 6 where both tools had some different features, but most of the differences are gone by now.
Therefore, we won't run both tools anymore in the CI.

We decided to stick with `phpstan` and remove `psalm` because:
* It's easier to write custom `phpstan` rules than to extend `psalm`
* We already have custom `phpstan` rules
* There are more extension for `phpstan`, e.g. for `symfony` or `phpunit`

## Consequences
`psalm` will be completely removed from the repository and the CI.

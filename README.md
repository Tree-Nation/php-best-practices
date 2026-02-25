# PHP Best Practices Skill

This repository contains a Codex skill that standardizes how PHP backend code is created and refactored using TreeNation's Domain-Driven Design conventions.

## What this includes

- Skill definition: `skills/php-best-practices/SKILL.md`
- Skill guidance: `skills/php-best-practices/AGENTS.md`
- Rule set: `skills/php-best-practices/rules/*.md`

## Purpose

Use this skill when working on PHP backend components such as:

- Controllers and request validation classes
- DTOs
- Services and service responses
- Repository interfaces and Eloquent implementations
- Dependency-injection bindings
- Unit tests for services

## Core conventions enforced

- Keep controllers thin; move business logic into services.
- Use strict typing in all new PHP files.
- Use invokable controllers for single actions.
- Use immutable DTOs when parameter complexity warrants it.
- Use repository interfaces in the domain layer and Eloquent implementations in infrastructure.
- Build repository queries via the Criteria pattern.
- Register repository bindings in `app/Providers/TreeNationProvider.php`.
- Unit-test services by mocking dependencies.

## Rule catalog

- `rules/thin-controllers.md`
- `rules/invokable-controllers.md`
- `rules/request-validation-class.md`
- `rules/when-to-use-dtos.md`
- `rules/immutable-dtos.md`
- `rules/service-business-logic.md`
- `rules/service-response-pattern.md`
- `rules/repository-interface.md`
- `rules/eloquent-repository-implementation.md`
- `rules/criteria-pattern.md`
- `rules/register-bindings.md`
- `rules/unit-test-services.md`

## Suggested workflow

1. Identify which layer(s) are changing.
2. Open only the relevant rule files for that task.
3. Implement the smallest architecture-compliant change.
4. Register new repository bindings when interfaces are added.
5. Validate with PHP CS Fixer and PHPStan.

## Repository layout

```text
skills/
  php-best-practices/
    SKILL.md
    AGENTS.md
    rules/
      *.md
```

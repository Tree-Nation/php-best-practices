# Model Property Access via Getters

## Why

Accessing Eloquent model properties directly (e.g. `$action->id`) bypasses any accessor logic defined on the model and makes the code harder to refactor. Using getter methods (or Eloquent accessors) keeps the access point consistent and explicit.

## Pattern

Define an accessor on the model (Laravel's `Attribute` casting or a plain getter method):

```php
// app/Models/Action.php
use Illuminate\Database\Eloquent\Casts\Attribute;

final class Action extends Model
{
    public function id(): Attribute
    {
        return Attribute::get(fn () => $this->attributes['id']);
    }

    public function title(): Attribute
    {
        return Attribute::get(fn () => $this->attributes['title']);
    }
}
```

Then access via the getter in services and response objects:

```php
// src/API/Habit/Application/Services/GetActionDetailService.php
return new GetActionDetailResponse(
    id: $action->id(),
    title: $action->title(),
    description: $action->description(),
);
```

## Checklist

- **Do not access model properties directly** (e.g. `$action->id`, `$action->title`) inside services or response constructors.
- Use getter methods or Eloquent `Attribute` accessors instead.
- If the model does not yet have a getter for the property you need, add one before using it.
- This applies when building response objects, DTOs, and any other place where model data is mapped to another structure.

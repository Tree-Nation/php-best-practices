# Request Validation Class

## Why

Separating validation from the controller keeps the controller thin and makes the validation rules easy to test and reuse.

## Pattern

```php
// app/Http/Controllers/[Domain]/[Action]Request.php
class GetHashtagsRequest extends FormRequest
{
    public function authorize(): bool
    {
        return true;
    }

    public function rules(): array
    {
        return [
            'featured' => 'sometimes|in:true,false',
            'trending' => 'sometimes|in:true,false',
            'hashtag' => 'sometimes|string',
            'limit' => 'sometimes|integer|min:1|max:100',
            'showHashtagOfTheDay' => 'sometimes|in:true,false',
            'excludeHashtag' => 'sometimes|string',
        ];
    }
}
```

## Checklist

- Extend `Illuminate\Foundation\Http\FormRequest`.
- Place in the same directory as the controller: `app/Http/Controllers/[Domain]/`.
- Use `sometimes` for optional query parameters.
- Use `in:true,false` for boolean query parameters (they arrive as strings in GET requests).
- Use `boolean()` / `integer()` / `input()` helpers in the controller to cast values.
- `authorize()` returns `true` by default; add real auth logic only when required.
- No business logic in `rules()`.

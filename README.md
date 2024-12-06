# Developer Notes Repository

Welcome to my repository of useful coding snippets and reminders!

# SQL Replace for Hyphen-Insensitive Searches

When you need to search a MySQL column while ignoring hyphens, you can use the `REPLACE` function to strip hyphens (`-`) from the database column during the comparison. This is especially useful when user input may include misplaced or omitted hyphens.

## Laravel Example

```php
$artisans = Artisans::orderBy('name');
if (Session::has('query')) {
    $userInput = str_replace('-', '', Session::get('query')); // Remove hyphens from user input
    $artisans->where(function ($query) use ($userInput) {
        $query->where('name', 'like', '%' . Session::get('query') . '%')
              ->orWhere('momo_number', 'like', '%' . Session::get('query') . '%')
              ->orWhereRaw("REPLACE(code, '-', '') LIKE ?", ['%' . $userInput . '%']);
    });
}
$artisans = $artisans->paginate(30);

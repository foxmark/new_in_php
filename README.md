# New in PHP
## Traits

```php
trait Commentable
{
    public function addComment($something)
    {
        // ...
    }
}

class Post
{
    use Commentable;
}

class Image
{
    use Commentable;
}
```

## Array destructuring

```php
[$a, $b] = ["a", "b"];
```

## Variadic functions

```php
function sum(...$nums)
{
    return array_sum($nums);
}

sum(1);
sum(1, 2);
sum(1, 2, 3);
```

```php
function add($a, $b, $c)
{
    return $a + $b + $c;
}

$rest = [2, 3];
add(1, ...$rest);
```
## Join arrays

```php
$chunk1 = [3, 5, 7];
$chunk2 = [11, 13, 17];

$numbers = [2, ...$chunk1, ...$chunk2, 18, 19, 20];
```

## Generators

```php
function lines($filename)
{
    $f = fopen($filename, 'r');
    while(($line = fgets($f)) !== false) {
        yield $line;
    }
    fclose($f);
}
```

## Arrow functions

```php
array_map(function ($user) {
    return $user->id;
}, $users);

array_map(fn($user) => $user->id, $users);
```
## Null coalescing

```php
$user['name'] = $user['name'] ?? 'Guest';
```

## null coalescing assignment
```php
$user['name'] ??= 'Guest';
```

## Null chaining operator

```php
// before
$birthday = $user->birthday;
$birthday = $birthday ? $birthday->format('Y-m-d') : null;

// now
$birthday = $user->birthday?->format('Y-m-d');
```
## Named arguments

```php
function createUser($name, $email, $language = null, $country = null)
{
    //
}

createUser(
    name: 'Mike',
    email: 'user@server.com',
    country: 'UK'
);
```

## Non-capturing catch

```php
// before
try {

} catch (Exception $e) {
    return false;
}

// now
try {

} catch (Exception) {
    return false;
}
```

## Sensitive parameter attribute

```php
function login($user, #[SensitiveParameter] $password)
{
    throw new Exception('Error');
}
```
## Match statements (case)

```php
$message = match (statusCode) {
    200,300 => null,
    400 => 'not found',
    500 => 'server error',
    default => 'unknown status code',
}
```
## Enums

```php
enum Status
{
    case DRAFT;
    case ACTIVE;
    case DELETED;
}
// or even
enum Status: int
{
    case DRAFT = 1;
    case ACTIVE = 2;
    case DELETED = 3;
}
```

```php

enum Status
{
    case DRAFT;
    case ACTIVE;
    case DELETED;

    public function display()
    {
        return match ($this) {
            Status::DRAFT => 'Draft',
            Status::ACTIVE => 'Active',
            Status::DELETED => 'Deleted',
        };
    }
}

class BlogPost
{
    public function setStatus(Status $status)
    {
        //
    }
}
```

## Typehints

```php

function add(int $a, int $b): int
{
    return $a + $b;
}

```
```php

function add(int|float $a, int|float $b): int|float
{
    return $a + $b;
}

```

```php

class Typed
{
    // type Foo OR type Bar
    public function run(Foo|Bar $input)
    {

    }
}
```

```php

class Typed
{
    // type Foo AND type Bar
    public function run(Foo&Bar $input)
    {
        
    }
}
```

```php

class Typed
{
    // type Foo AND type Bar OR NULL
    public function run((Foo&Bar)|null $input)
    {
        
    }
}
```

## Typed properties

```php

class Typed
{
    public string $title;

    public DateTime $date;

    public function __construct(string $title, DateTime $date)
    {
        $this->title = $title;
        $this->date = $date;
    }
}
```

```php
// constructor promotion
class Typed
{
    public function __construct(public string $title, public DateTime $date)
    {
        //
    }
}
```

```php
// constructor promotion - readonly
class Typed
{
    public function __construct(public readonly string $title, public readonly DateTime $date)
    {
        //
    }
}
```

```php
// constructor promotion - readonly class level
readonly class Typed
{
    public function __construct(public  string $title, public DateTime $date)
    {
        //
    }
}
```

# PHP Practical Guide - Grade 3 Applied Technology Schools

Welcome to the ultimate PHP hands-on guide! This documentation covers all practical workshops for **Unit 19 (PHP Level 1)**, designed specifically to help 3rd-grade students master PHP programming concepts easily and achieve top grades.

---

## 📚 Table of Contents
1. [Workshop 1: Basic PHP & Logic](#workshop-1-basic-php--logic)
2. [Workshop 2: Control Structures & Loops](#workshop-2-control-structures--loops)
3. [Workshop 3: Functions & Array Operations](#workshop-3-functions--array-operations)
4. [Workshop 4: Modular PHP & Form Handling](#workshop-4-modular-php--form-handling)
5. [Workshop 5: Database Operations with MySQLi](#workshop-5-database-operations-with-mysqli)

---

## Workshop 1: Basic PHP & Logic

### Task 2: Basic PHP Syntax, Operators & Logic

#### 📌 Problem Description
Create a file named `task.php` in your project folder that performs the following:
1. Define a constant named `PASSING_GRADE` with a value of `50`.
2. Create two variables `$num1` and `$num2` with numeric values, and output the results of their addition, subtraction, multiplication, and division.
3. Create a variable `$studentGrade` (e.g., `65`), compare it to `PASSING_GRADE`, and display whether the student passed (`true`/`false`).
4. Use a logical operator (`&&` or `||`) to check two conditions together (e.g., the student is passing AND older than 18).

---

#### 💻 Full Solution Code
```php
<?php
// 1. Define a constant
define("PASSING_GRADE", 50);

// 2. Math operations with variables
$num1 = 12;
$num2 = 4;

echo "Sum: " . ($num1 + $num2) . "\n";
echo "Difference: " . ($num1 - $num2) . "\n";
echo "Product: " . ($num1 * $num2) . "\n";
echo "Division: " . ($num1 / $num2) . "\n";

// 3. Comparison check
$studentGrade = 65;
$age = 20;

echo "Is Passing: " . ($studentGrade >= PASSING_GRADE ? "true" : "false") . "\n";

// 4. Logical combination
echo "Passing and Adult: " . (($studentGrade >= PASSING_GRADE && $age > 18) ? "true" : "false");
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Define Constants**
  We use `define("PASSING_GRADE", 50);` to store a fixed value that cannot be changed during code execution.

* **Step 2: Arithmetic Operations**
  We store numbers in variables `$num1` and `$num2`. We use PHP math symbols (`+`, `-`, `*`, `/`) and combine text with variables using the dot operator (`.`).

* **Step 3: Ternary Comparison**
  `$studentGrade >= PASSING_GRADE` checks if the score is greater than or equal to 50. The ternary operator `? "true" : "false"` prints the string "true" if the condition succeeds, otherwise "false".

* **Step 4: Logical AND Operator**
  The `&&` symbol means **BOTH** conditions must be true:
  1. `$studentGrade >= PASSING_GRADE` (Grade is 50+)
  2. `$age > 18` (Age is above 18)

---

## Workshop 2: Control Structures & Loops

### Task 1: FizzBuzz with a Twist

#### 📌 Problem Description
Write `task1.php` that loops from 1 to 50:
- Prints `"Fizz"` if divisible by 3.
- Prints `"Buzz"` if divisible by 5.
- Prints `"FizzBuzz"` if divisible by both 3 and 5.
- Otherwise, prints the number itself.
- **Twist:** If the number is a **prime number**, enclose the output in square brackets `[]` (e.g., `[2]`, `[7]`, `[Fizz]`).

---

#### 💻 Full Solution Code
```php
<?php
// Function to check if a number is prime
function isPrime($n) {
    if ($n < 2) return false;
    for ($i = 2; $i <= sqrt($n); $i++) {
        if ($n % $i == 0) return false;
    }
    return true;
}

// Loop from 1 to 50
for ($i = 1; $i <= 50; $i++) {
    if ($i % 3 == 0 && $i % 5 == 0) {
        $output = "FizzBuzz";
    } elseif ($i % 3 == 0) {
        $output = "Fizz";
    } elseif ($i % 5 == 0) {
        $output = "Buzz";
    } else {
        $output = $i;
    }

    // Check if the current number is prime and print formatted output
    echo isPrime($i) ? "[$output]" : $output;
    echo "\n";
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Create Prime Helper Function**
  A prime number is greater than 1 and divisible only by 1 and itself. We create a loop from 2 up to the square root of `$n` (`sqrt($n)`) to check if any number divides `$n` without a remainder (`%`).

* **Step 2: Iterate with a For Loop**
  `for ($i = 1; $i <= 50; $i++)` repeats the logic for all numbers between 1 and 50.

* **Step 3: Evaluate Modulo `%` Conditions**
  - Check `$i % 3 == 0 && $i % 5 == 0` first because divisible by both 3 and 5 is a specific case.
  - Then check individual divisibility by 3 (`Fizz`) and 5 (`Buzz`).

* **Step 4: Format Brackets for Prime Numbers**
  We pass the loop counter `$i` to `isPrime($i)`. If true, we wrap `$output` with `[]`.

---

### Task 2: Grade Report with Validation

#### 📌 Problem Description
Given an array of raw values: `$scores = [95, "abc", 72, -5, 105, 60, "88"];`
Write `task2.php` to loop through each item:
1. If not a valid number, print `"Invalid entry: <value>"`.
2. If numeric but out of valid grade range (`< 0` or `> 100`), print `"Out of range: <value>"`.
3. For valid numbers, classify them using `switch(true)`:
   - 90–100 -> **A**
   - 75–89 -> **B**
   - 60–74 -> **C**
   - Below 60 -> **F**
4. Print: `Score <number> -> <Grade>`

---

#### 💻 Full Solution Code
```php
<?php
$scores = [95, "abc", 72, -5, 105, 60, "88"];

foreach ($scores as $score) {
    // 1. Check if input is non-numeric
    if (!is_numeric($score)) {
        echo "Invalid entry: $score\n";
        continue;
    }

    $score = (float)$score;

    // 2. Check if score is outside valid boundaries
    if ($score < 0 || $score > 100) {
        echo "Out of range: $score\n";
        continue;
    }

    // 3. Evaluate grade range using switch (true) pattern
    switch (true) {
        case $score >= 90:
            $grade = "A";
            break;
        case $score >= 75:
            $grade = "B";
            break;
        case $score >= 60:
            $grade = "C";
            break;
        default:
            $grade = "F";
    }

    echo "Score $score -> $grade\n";
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Iterate Array with `foreach`**
  `foreach ($scores as $score)` visits every entry in the raw dataset one by one.

* **Step 2: Validate Data Type with `is_numeric()`**
  If `!is_numeric($score)` is true (like `"abc"`), we print an invalid message and call `continue;` to immediately skip to the next loop item.

* **Step 3: Validate Boundaries**
  If `$score < 0 || $score > 100` is true (like `-5` or `105`), we print an out-of-range message and skip using `continue;`.

* **Step 4: The `switch (true)` Trick**
  Normally, PHP `switch` matches static values. By using `switch (true)`, PHP compares `true` against expressions like `$score >= 90`. The first expression that evaluates to `true` executes its corresponding `case`.

---

### Task 3: Inventory Management (Nested Loops & Associative Arrays)

#### 📌 Problem Description
Given a multi-dimensional array representing warehouse items:
```php
$warehouse = [
    "Electronics" => ["Laptop" => 5, "Phone" => 0, "Tablet" => 12],
    "Furniture"   => ["Chair" => 20, "Desk" => 0, "Sofa" => 3],
    "Stationery"  => ["Pen" => 500, "Notebook" => 0, "Stapler" => 8]
];
```
Write `task3.php` to:
1. Loop through each category and item using nested `foreach` loops.
2. Skip 0-stock items using `continue;`, but count them as out-of-stock items.
3. Print items in stock as: `Electronics - Laptop: 5 units`.
4. Output a summary showing total categories, items in stock, and items out of stock.

---

#### 💻 Full Solution Code
```php
<?php
$warehouse = [
    "Electronics" => ["Laptop" => 5, "Phone" => 0, "Tablet" => 12],
    "Furniture"   => ["Chair" => 20, "Desk" => 0, "Sofa" => 3],
    "Stationery"  => ["Pen" => 500, "Notebook" => 0, "Stapler" => 8]
];

$inStockCount = 0;
$outOfStockCount = 0;

foreach ($warehouse as $category => $items) {
    foreach ($items as $item => $stock) {
        if ($stock == 0) {
            $outOfStockCount++;
            continue;
        }
        echo "$category - $item: $stock units\n";
        $inStockCount++;
    }
}

echo "\nSummary:\n";
echo "Categories: " . count($warehouse) . "\n";
echo "Items in stock: $inStockCount\n";
echo "Items out of stock: $outOfStockCount\n";
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Setup Tracking Counters**
  Define `$inStockCount = 0;` and `$outOfStockCount = 0;` before the loop starts.

* **Step 2: Outer `foreach` Loop**
  `foreach ($warehouse as $category => $items)` extracts the category string (key) and the nested array of items (value).

* **Step 3: Inner `foreach` Loop**
  `foreach ($items as $item => $stock)` iterates through each product and its current stock value inside that category.

* **Step 4: Zero Stock Handling**
  If `$stock == 0`, increment `$outOfStockCount++` and skip output with `continue;`.

* **Step 5: Output Summary Statistics**
  `count($warehouse)` calculates total outer categories.

---

### Task 4: Number Guessing Game Logic (`do...while` + `break`)

#### 📌 Problem Description
Simulate a number guessing game in `task4.php`:
- Target number: `$secretNumber = 42;`
- Array of guesses: `$guesses = [10, 55, 30, 42, 99];`
- Use a `do...while` loop to evaluate each guess from the array.
- Output `"Too low"`, `"Too high"`, or `"Correct!"`.
- Stop immediately when the correct guess is found using `break;`.
- Output total attempts taken or `"Out of guesses!"` if not found.

---

#### 💻 Full Solution Code
```php
<?php
$secretNumber = 42;
$guesses = [10, 55, 30, 42, 99];
$guessIndex = 0;
$attempts = 0;
$found = false;

do {
    $guess = $guesses[$guessIndex];
    $attempts++;

    if ($guess < $secretNumber) {
        echo "$guess: Too low\n";
    } elseif ($guess > $secretNumber) {
        echo "$guess: Too high\n";
    } else {
        echo "$guess: Correct!\n";
        $found = true;
        break;
    }

    $guessIndex++;
} while ($guessIndex < count($guesses));

if ($found) {
    echo "Found it in $attempts attempts.\n";
} else {
    echo "Out of guesses!\n";
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Initialize Control Variables**
  We set `$guessIndex` to traverse the array index from 0, and `$found` flag as `false`.

* **Step 2: Execute `do...while` Loop**
  A `do...while` loop guarantees execution at least once before checking the loop condition `$guessIndex < count($guesses)`.

* **Step 3: Evaluate Target vs Guess**
  Compare current guess `$guess` against `$secretNumber` using conditional checks (`<`, `>`).

* **Step 4: Break Execution on Success**
  When `$guess == $secretNumber`, set `$found = true;` and terminate the loop immediately with `break;` so remaining numbers are ignored.

---

### Task 5: Simple Text-Based Calculator with Switch & Error Handling

#### 📌 Problem Description
Write `task5.php` that iterates through an array of math operation items:
```php
$operations = [
    ["num1" => 10, "num2" => 5, "op" => "+"],
    ["num1" => 10, "num2" => 0, "op" => "/"],
    ["num1" => 7,  "num2" => 3, "op" => "*"],
    ["num1" => 9,  "num2" => 2, "op" => "%"],
    ["num1" => 5,  "num2" => 5, "op" => "^"]
];
```
Requirements:
1. Support operators: `+`, `-`, `*`, `/`, `%`.
2. Handle division by zero gracefully without runtime crashing.
3. Catch unsupported operators using `default`.

---

#### 💻 Full Solution Code
```php
<?php
$operations = [
    ["num1" => 10, "num2" => 5, "op" => "+"],
    ["num1" => 10, "num2" => 0, "op" => "/"],
    ["num1" => 7,  "num2" => 3, "op" => "*"],
    ["num1" => 9,  "num2" => 2, "op" => "%"],
    ["num1" => 5,  "num2" => 5, "op" => "^"]
];

foreach ($operations as $operation) {
    $a  = $operation["num1"];
    $b  = $operation["num2"];
    $op = $operation["op"];

    switch ($op) {
        case "+":
            echo "$a + $b = " . ($a + $b) . "\n";
            break;
        case "-":
            echo "$a - $b = " . ($a - $b) . "\n";
            break;
        case "*":
            echo "$a * $b = " . ($a * $b) . "\n";
            break;
        case "/":
            if ($b == 0) {
                echo "Error: division by zero\n";
            } else {
                echo "$a / $b = " . ($a / $b) . "\n";
            }
            break;
        case "%":
            if ($b == 0) {
                echo "Error: division by zero\n";
            } else {
                echo "$a % $b = " . ($a % $b) . "\n";
            }
            break;
        default:
            echo "Error: unknown operator $op\n";
    }
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Unpack Data in Loop**
  In each iteration, extract values `$a`, `$b`, and operator string `$op` into simple local variables.

* **Step 2: Dispatch Operations via `switch`**
  The `switch($op)` compares the string stored inside `$op` to each operator case.

* **Step 3: Division by Zero Prevention**
  Inside `/` and `%` cases, check `if ($b == 0)` before computing math to avoid PHP zero-division errors.

* **Step 4: Handle Unknown Symbols**
  `default:` catches any unsupported operators (like `^`) and outputs an explicit error message.

---

## Workshop 3: Functions & Array Operations

### Task 1: String Utility Toolkit

#### 📌 Problem Description
Create `task1.php` containing a function `formatUsername($fullName, $maxLength = 10)` that:
1. Converts `$fullName` to lowercase.
2. Replaces spaces with underscores `_`.
3. Truncates text exceeding `$maxLength` using `substr()`, adding `"..."` at the end.
4. Returns the formatted username string.
5. Test it with at least 3 names (including default parameter usage and truncation).

---

#### 💻 Full Solution Code
```php
<?php
function formatUsername($fullName, $maxLength = 10) {
    $formatted = strtolower($fullName);
    $formatted = str_replace(" ", "_", $formatted);

    if (strlen($formatted) > $maxLength) {
        $formatted = substr($formatted, 0, $maxLength) . "...";
    }

    return $formatted;
}

// Testing the function
echo formatUsername("Ahmed Hassan") . "\n"; // Default length 10 -> ahmed_hass...
echo formatUsername("Sara Ali", 5) . "\n";    // Custom length 5 -> sara_...
echo formatUsername("Bob") . "\n";            // Short name -> bob
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Function Definition with Default Argument**
  `$maxLength = 10` defines a default parameter value used if the caller omits the second argument.

* **Step 2: String Manipulations**
  - `strtolower()` converts all characters to lowercase.
  - `str_replace(" ", "_", ...)` substitutes spaces with underscores.

* **Step 3: Length Validation & Substring Truncation**
  - `strlen()` measures total string characters.
  - If length exceeds `$maxLength`, `substr($formatted, 0, $maxLength)` cuts characters starting from position 0 up to `$maxLength`, and appends `"..."`.

* **Step 4: Return Value**
  Return the processed string so callers can display or reuse it.

---

### Task 2: Number Analyzer with Arrow Functions

#### 📌 Problem Description
Given `$numbers = [4.7, -12, 9, 25.3, -3.9, 16, 1.1];`
Write `task2.php` utilizing PHP **Arrow Functions** (`fn($n) => ...`) to:
1. Calculate absolute values for all numbers.
2. Round each number to its nearest integer.
3. Compute square root of positive numbers only (`>= 0`).
4. Find min, max, and maximum value squared ($max^2$).

---

#### 💻 Full Solution Code
```php
<?php
$numbers = [4.7, -12, 9, 25.3, -3.9, 16, 1.1];

// 1. Absolute values
$absolutes = array_map(fn($n) => abs($n), $numbers);

// 2. Rounded numbers
$rounded = array_map(fn($n) => round($n), $numbers);

// 3. Square roots (Positive numbers only)
$sqrtsOfPositive = array_map(fn($n) => $n >= 0 ? sqrt($n) : null, $numbers);
$filteredSqrts   = array_filter($sqrtsOfPositive, fn($v) => $v !== null);

// Output results
echo "Absolute values: " . implode(", ", $absolutes) . "\n";
echo "Rounded: " . implode(", ", $rounded) . "\n";
echo "Square roots (positives only): " . implode(", ", $filteredSqrts) . "\n";

// 4. Min, Max, and Max Squared
$max = max($numbers);
echo "Min: " . min($numbers) . "\n";
echo "Max: " . $max . "\n";
echo "Max squared: " . pow($max, 2) . "\n";
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Arrow Functions with `array_map()`**
  `array_map(fn($n) => abs($n), $numbers)` applies the short arrow function to every item in the `$numbers` array.

* **Step 2: Positive Number Filtering**
  We map negative numbers to `null`, then use `array_filter($array, fn($v) => $v !== null)` to strip out all `null` values.

* **Step 3: Built-in Math Functions**
  - `min()` finds the lowest value.
  - `max()` finds the highest value.
  - `pow($max, 2)` calculates $max^2$.
  - `implode(", ", $array)` converts output arrays to readable strings for display.

---

### Task 3: Student Records with Associative & Multidimensional Arrays

#### 📌 Problem Description
Given a multi-dimensional array of students:
```php
$students = [
    ["name" => "Layla", "scores" => [88, 92, 79]],
    ["name" => "Omar",  "scores" => [65, 70, 60]],
    ["name" => "Nour",  "scores" => [95, 89, 99]]
];
```
Write `task3.php` to:
1. Create a function `calculateAverage($scores)` using `array_sum()` and `count()` (no built-in average function).
2. Loop through `$students` and print each average rounded to 2 decimals.
3. Identify and print the top-performing student name and average.

---

#### 💻 Full Solution Code
```php
<?php
$students = [
    ["name" => "Layla", "scores" => [88, 92, 79]],
    ["name" => "Omar",  "scores" => [65, 70, 60]],
    ["name" => "Nour",  "scores" => [95, 89, 99]]
];

// Custom function to calculate array average
function calculateAverage($scores) {
    return array_sum($scores) / count($scores);
}

$topStudent = "";
$topAverage = 0;

foreach ($students as $student) {
    $avg = round(calculateAverage($student["scores"]), 2);
    echo $student["name"] . " Average: " . $avg . "\n";

    if ($avg > $topAverage) {
        $topAverage = $avg;
        $topStudent = $student["name"];
    }
}

echo "\nTop student: $topStudent with an average of $topAverage\n";
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Build Custom Average Calculation**
  `array_sum($scores)` adds all score values, and `count($scores)` returns total item count. Dividing sum by total gives the exact average.

* **Step 2: Round Results**
  `round(..., 2)` limits float numbers to 2 decimal places.

* **Step 3: Determine Top Performer**
  We compare current `$avg` with `$topAverage`. If higher, update `$topAverage` and assign `$topStudent = $student["name"]`.

---

### Task 4: Inventory Manager Using Array Functions

#### 📌 Problem Description
Write `task4.php` starting with:
`$stock = ["Laptop", "Phone", "Tablet"];`
`$newArrivals = ["Monitor", "Keyboard"];`
Execute operations sequentially:
1. Add `"Mouse"` to end of `$stock` via `array_push()`.
2. Remove last item via `array_pop()` and print it.
3. Check if `"Tablet"` exists via `in_array()`.
4. Merge `$stock` and `$newArrivals` into `$fullCatalog` via `array_merge()`.
5. Slice first 3 items via `array_slice()`.
6. Print `$fullCatalog` in reverse order via `array_reverse()` without changing original array.

---

#### 💻 Full Solution Code
```php
<?php
$stock = ["Laptop", "Phone", "Tablet"];
$newArrivals = ["Monitor", "Keyboard"];

// 1. Add item to end
array_push($stock, "Mouse");
echo "After adding Mouse: " . implode(", ", $stock) . "\n";

// 2. Remove last item
$removed = array_pop($stock);
echo "Removed: $removed\n";
echo "After removing: " . implode(", ", $stock) . "\n";

// 3. Check item existence
$hasTablet = in_array("Tablet", $stock);
echo "Tablet in stock? " . ($hasTablet ? "Yes" : "No") . "\n";

// 4. Merge arrays
$fullCatalog = array_merge($stock, $newArrivals);
echo "Full catalog: " . implode(", ", $fullCatalog) . "\n";

// 5. Slice array
$firstThree = array_slice($fullCatalog, 0, 3);
echo "First 3 items: " . implode(", ", $firstThree) . "\n";

// 6. Reverse array display
$reversed = array_reverse($fullCatalog);
echo "Reversed (original untouched): " . implode(", ", $reversed) . "\n";
echo "Original still: " . implode(", ", $fullCatalog) . "\n";
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Modify End Elements**
  - `array_push($stock, "Mouse")` adds "Mouse" at array index end.
  - `array_pop($stock)` removes and returns the last element ("Mouse").

* **Step 2: Existence Search**
  `in_array("Tablet", $stock)` returns `true` if item exists in `$stock`.

* **Step 3: Array Combination & Slicing**
  - `array_merge($stock, $newArrivals)` combines elements into one list.
  - `array_slice($fullCatalog, 0, 3)` extracts 3 items starting at index offset 0.

* **Step 4: Non-Destructive Reversal**
  `array_reverse()` returns a new inverted array while preserving `$fullCatalog` in its original order.

---

### Task 5: Mini Contact Book with Callback Functions

#### 📌 Problem Description
Create `task5.php` with:
1. `addContact($book, $name, $phone)` function: adds entry `["phone" => $phone, "added_on" => date("Y-m-d")]` to associative array `$book` and returns it.
2. `searchContacts($book, $filterFn)` function: accepts array and anonymous callback function `$filterFn`, returning matching entries.
3. Filter contacts whose names start with letter `"L"` using `str_starts_with()`.

---

#### 💻 Full Solution Code
```php
<?php
function addContact($book, $name, $phone) {
    $book[$name] = [
        "phone" => $phone,
        "added_on" => date("Y-m-d")
    ];
    return $book;
}

function searchContacts($book, $filterFn) {
    $results = [];
    foreach ($book as $name => $info) {
        if ($filterFn($name)) {
            $results[$name] = $info;
        }
    }
    return $results;
}

// 1. Initialize and add contacts
$contacts = [];
$contacts = addContact($contacts, "Layla", "0123456789");
$contacts = addContact($contacts, "Omar",  "0111222333");
$contacts = addContact($contacts, "Laila", "0155566677");

// 2. Search using callback
$filtered = searchContacts($contacts, function($name) {
    return str_starts_with($name, "L");
});

// 3. Display output
foreach ($filtered as $name => $info) {
    echo "Name: $name, Phone: " . $info["phone"] . ", Added: " . $info["added_on"] . "\n";
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Immutable Parameter Modification**
  `addContact()` receives the array, updates key `$name` with nested associative info, and returns the modified array.

* **Step 2: Passing Functions as Arguments (Callbacks)**
  `searchContacts()` takes `$filterFn`. Inside the loop, calling `$filterFn($name)` executes the anonymous function passed during invocation.

* **Step 3: Matching Criteria**
  `str_starts_with($name, "L")` returns `true` if contact name starts with uppercase letter "L".

---

## Workshop 4: Modular PHP & Form Handling

### Task 1: Modular Page Structure with `include` / `require`

#### 📌 Problem Description
Build a multi-file modular layout:
1. `config.php`: Defines `SITE_NAME` constant.
2. `header.php`: Displays `<header>` tag with site title.
3. `footer.php`: Displays `<footer>` tag with current year via `date("Y")`.
4. `index.php`: Loads configurations using `require_once()`, header/footer using `include()`, and tests error behavior when files are missing.

---

#### 💻 Full Solution Code

**File 1: `config.php`**
```php
<?php
define("SITE_NAME", "My PHP Workshop");
?>
```

**File 2: `header.php`**
```php
<?php
echo "<header><h1>" . SITE_NAME . "</h1></header>";
?>
```

**File 3: `footer.php`**
```php
<?php
echo "<footer>© " . date("Y") . " " . SITE_NAME . "</footer>";
?>
```

**File 4: `index.php`**
```php
<?php
// require_once ensures critical file is loaded exactly once
require_once("config.php");
require_once("config.php"); // Second call is safely ignored

include("header.php");
echo "<p>Welcome to the site.</p>";
include("footer.php");
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Critical Files Loading (`require_once`)**
  `require_once("config.php")` stops script execution if `config.php` is missing. Calling it twice will not cause "constant already defined" errors because PHP tracks loaded files.

* **Step 2: Layout Inclusion (`include`)**
  `include("header.php")` injects template blocks. If an included file is missing, PHP shows a **Warning** but continues running the remaining page script.

* **Step 3: Difference Test**
  - If `include("missing.php")` fails $\rightarrow$ Output Warning, page continues rendering.
  - If `require("missing.php")` fails $\rightarrow$ Output Fatal Error, script execution terminates immediately.

---

### Task 2: GET vs POST Search & Login Forms

#### 📌 Problem Description
Build two form pages demonstrating correct HTTP methods:
1. `search.php`: Search query field using `GET` method. Reads `$_GET['q']`.
2. `login.php`: Credentials fields using `POST` method. Reads `$_POST['username']` and `$_POST['password']`.
3. Add explanatory comments justifying method selection.

---

#### 💻 Full Solution Code

**File 1: `search.php`**
```php
<!-- GET method is used for bookmarkable/search pages because query values appear visible in URL -->
<form method="GET" action="search.php">
    <input type="text" name="q" placeholder="Search...">
    <button type="submit">Search</button>
</form>

<?php
if (isset($_GET['q'])) {
    echo "You searched for: " . htmlspecialchars($_GET['q']);
}
?>
```

**File 2: `login.php`**
```php
<!-- POST method is used for sensitive forms to send data inside request body without URL visibility -->
<form method="POST" action="login.php">
    <input type="text" name="username" placeholder="Username">
    <input type="password" name="password" placeholder="Password">
    <button type="submit">Login</button>
</form>

<?php
if (isset($_POST['username']) && isset($_POST['password'])) {
    echo "Welcome, " . htmlspecialchars($_POST['username']);
    // SECURITY NOTE: Passwords must NEVER be printed back or logged to screen!
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Using `$_GET` for Searches**
  `GET` appends form parameters into URL query strings (e.g., `search.php?q=laptop`), making search result pages easily bookmarkable and shareable.

* **Step 2: Using `$_POST` for Authentication**
  `POST` hides user input inside the invisible HTTP request headers/body, keeping sensitive credentials like passwords out of browser location bars and server access logs.

* **Step 3: Safeguard Access with `isset()`**
  Checking `isset($_GET['q'])` prevents PHP notice warnings on initial page render before form submission.

---

### Task 3: Full Server-Side Form Validation

#### 📌 Problem Description
Build `register.php` validating form fields server-side:
- **name:** Not empty, minimum 2 characters.
- **email:** Valid format using `filter_var(..., FILTER_VALIDATE_EMAIL)`.
- **age:** Numeric value between 13 and 120.
- **website:** Optional, but if provided must be a valid URL.
- **password:** Minimum 8 characters.
- Collect **all** errors into an array before rendering messages to the user.

---

#### 💻 Full Solution Code
```php
<?php
$errors = [];
$success = false;

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $name     = $_POST['name'] ?? '';
    $email    = $_POST['email'] ?? '';
    $age      = $_POST['age'] ?? '';
    $website  = $_POST['website'] ?? '';
    $password = $_POST['password'] ?? '';

    // Validate Name
    if (empty($name) || strlen($name) < 2) {
        $errors[] = "Name must be at least 2 characters";
    }

    // Validate Email
    if (empty($email) || !filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $errors[] = "Please enter a valid email";
    }

    // Validate Age
    if (empty($age) || !is_numeric($age) || $age < 13 || $age > 120) {
        $errors[] = "Age must be between 13 and 120";
    }

    // Validate Optional Website
    if (!empty($website) && !filter_var($website, FILTER_VALIDATE_URL)) {
        $errors[] = "Website must be a valid URL";
    }

    // Validate Password
    if (empty($password) || strlen($password) < 8) {
        $errors[] = "Password must be at least 8 characters";
    }

    if (empty($errors)) {
        $success = true;
    }
}
?>

<form method="POST" action="register.php">
    Name: <input type="text" name="name"><br>
    Email: <input type="text" name="email"><br>
    Age: <input type="text" name="age"><br>
    Website (optional): <input type="text" name="website"><br>
    Password: <input type="password" name="password"><br>
    <button type="submit">Register</button>
</form>

<?php if (!empty($errors)): ?>
    <ul style="color:red;">
        <?php foreach ($errors as $error): ?>
            <li><?php echo htmlspecialchars($error); ?></li>
        <?php endforeach; ?>
    </ul>
<?php elseif ($success): ?>
    <p style="color:green;">Registration successful! Welcome, <?php echo htmlspecialchars($name); ?></p>
<?php endif; ?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Check Submission via Request Method**
  `$_SERVER['REQUEST_METHOD'] === 'POST'` ensures validation code executes only after submitting the form.

* **Step 2: Fallback Null Coalescing Operator (`??`)**
  `$_POST['name'] ?? ''` prevents key undefined index warnings if an input is missing from request data.

* **Step 3: Accumulate Errors Pattern**
  Instead of failing on first error, each invalid condition appends error message text into `$errors[]` array.

* **Step 4: Use PHP Native Filters**
  - `filter_var($email, FILTER_VALIDATE_EMAIL)` verifies standard address syntax.
  - `filter_var($website, FILTER_VALIDATE_URL)` verifies web link formats.

---

### Task 4: XSS-Safe Comment Box

#### 📌 Problem Description
Build `comments.php` demonstrating prevention of Cross-Site Scripting (XSS) attacks:
1. Form with a comment textarea submitted via POST.
2. Render existing comments to the screen.
3. Compare raw unsafe output against sanitized output using `htmlspecialchars()`.
4. Explain how `htmlspecialchars()` prevents script injection attacks.

---

#### 💻 Full Solution Code
```php
<?php
$comments = ["Great tutorial!", "Looking forward to more."];

if ($_SERVER['REQUEST_METHOD'] === 'POST' && !empty($_POST['comment'])) {
    $comments[] = $_POST['comment'];
}
?>

<form method="POST" action="comments.php">
    <textarea name="comment" placeholder="Write a comment..."></textarea><br>
    <button type="submit">Post Comment</button>
</form>

<h3>Comments:</h3>
<ul>
<?php foreach ($comments as $comment): ?>
    <!-- 
      UNSAFE VERSION (DO NOT USE IN PRODUCTION):
      If user enters <script>alert('hacked')</script>, the browser executes script!
      <li><?php echo $comment; ?></li>
    -->

    <!-- 
      SAFE VERSION:
      htmlspecialchars() converts special symbols like < and > into &lt; and &gt;
      This causes the browser to print raw text tags instead of executing code.
    -->
    <li><?php echo htmlspecialchars($comment); ?></li>
<?php endforeach; ?>
</ul>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Receive User Input**
  Read text input submitted inside `$_POST['comment']`.

* **Step 2: Understand the Vulnerability**
  Printing raw text user input directly like `echo $comment;` enables malicious visitors to input `<script>alert('hack')</script>`. The browser parses the tags as executable JavaScript code.

* **Step 3: Escape HTML Entities**
  `htmlspecialchars($comment)` escapes special characters:
  - `<` becomes `&lt;`
  - `>` becomes `&gt;`
  - `&` becomes `&amp;`
  
  The browser displays harmless visible text `<script>` on screen instead of running malicious scripts.

---

## Workshop 5: Database Operations with MySQLi

### Database Setup Script
Execute this SQL schema inside MySQL / phpMyAdmin before starting:
```sql
CREATE DATABASE workshop_db;
USE workshop_db;

CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

### Task 1: Connect & Seed Database

#### 📌 Problem Description
1. Create `connect.php`: Connects to database `workshop_db` via `mysqli_connect()`. Handles errors with `mysqli_connect_error()` and prints MySQL version on success.
2. Create `seed.php`: Includes `connect.php` and executes 5 separate `INSERT INTO` queries to populate product data.

---

#### 💻 Full Solution Code

**File 1: `connect.php`**
```php
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db   = "workshop_db";

$conn = mysqli_connect($host, $user, $pass, $db);

if (!$conn) {
    die("Connection failed: " . mysqli_connect_error());
}

echo "Connected successfully. MySQL server version: " . mysqli_get_server_info($conn) . "\n";
?>
```

**File 2: `seed.php`**
```php
<?php
require_once("connect.php");

$products = [
    ["name" => "Laptop",     "price" => 899.99, "quantity" => 10],
    ["name" => "Mouse",      "price" => 15.50,  "quantity" => 100],
    ["name" => "Keyboard",   "price" => 45.00,  "quantity" => 60],
    ["name" => "Monitor",    "price" => 199.99, "quantity" => 25],
    ["name" => "Headphones", "price" => 59.99,  "quantity" => 40],
];

foreach ($products as $product) {
    $name  = $product['name'];
    $price = $product['price'];
    $qty   = $product['quantity'];

    $sql = "INSERT INTO products (name, price, quantity) VALUES ('$name', $price, $qty)";

    if (mysqli_query($conn, $sql)) {
        echo "Inserted: $name\n";
    } else {
        echo "Error inserting $name: " . mysqli_error($conn) . "\n";
    }
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Open MySQL Connection**
  `mysqli_connect($host, $user, $pass, $db)` establishes a link to the MySQL database server.

* **Step 2: Validate Connection**
  If `$conn` returns `false`, `die(mysqli_connect_error())` aborts execution and prints detailed driver error logs.

* **Step 3: Execute SQL Queries**
  `mysqli_query($conn, $sql)` executes SQL statements against the active database connection.

---

### Task 2: Product Catalog Reader with Dynamic Filters

#### 📌 Problem Description
Build `catalog.php` (includes `connect.php`) reading URL parameters:
- `?min_price=50`: Shows products with price $\ge 50$.
- `?sort=price_desc`: Sorts price descending; defaults to sorting by name ascending.
- Iterate results using `mysqli_fetch_assoc()`.
- Display combined total inventory dollar value ($\sum price \times quantity$).

---

#### 💻 Full Solution Code
```php
<?php
require_once("connect.php");

$sql = "SELECT * FROM products WHERE 1=1";

// Dynamic Filter
if (isset($_GET['min_price']) && is_numeric($_GET['min_price'])) {
    $minPrice = (float)$_GET['min_price'];
    $sql .= " AND price >= $minPrice";
}

// Dynamic Sorting
if (isset($_GET['sort']) && $_GET['sort'] === 'price_desc') {
    $sql .= " ORDER BY price DESC";
} else {
    $sql .= " ORDER BY name ASC";
}

$result = mysqli_query($conn, $sql);

if (!$result) {
    die("Query failed: " . mysqli_error($conn));
}

$totalCount = 0;
$totalValue = 0;

while ($row = mysqli_fetch_assoc($result)) {
    echo $row['name'] . " - $" . $row['price'] . " (Qty: " . $row['quantity'] . ")\n";
    $totalCount++;
    $totalValue += ($row['price'] * $row['quantity']);
}

echo "\nTotal products shown: $totalCount\n";
echo "Total inventory value shown: $" . number_format($totalValue, 2) . "\n";
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Construct Dynamic SQL (`WHERE 1=1`)**
  Starting base string with `WHERE 1=1` lets us safely append `AND ...` query clauses dynamically based on active filter parameters.

* **Step 2: Fetch Rows sequentially**
  `while ($row = mysqli_fetch_assoc($result))` converts each database record row into an associative array until all records are read.

* **Step 3: Format Financial Totals**
  `number_format($totalValue, 2)` formats floating numbers into standard currency string notation with two decimal places.

---

### Task 3: Update Stock with Transaction Logic

#### 📌 Problem Description
Create `restock.php` simulating stock shipment intake:
```php
$shipment = ["Laptop" => 5, "Mouse" => 50, "Drone" => 20];
```
1. Verify if item exists using `SELECT`.
2. If item exists, run `UPDATE` query adding quantity value (`quantity = quantity + X`). Check affected rows with `mysqli_affected_rows()`.
3. If item does not exist, print `"Skipped: <name> product not found"`.

---

#### 💻 Full Solution Code
```php
<?php
require_once("connect.php");

$shipment = [
    "Laptop" => 5,
    "Mouse"  => 50,
    "Drone"  => 20 // Product does not exist
];

foreach ($shipment as $name => $amount) {
    // 1. Verify product existence
    $checkSql    = "SELECT * FROM products WHERE name = '$name'";
    $checkResult = mysqli_query($conn, $checkSql);

    if (mysqli_num_rows($checkResult) === 0) {
        echo "Skipped: $name (product not found)\n";
        continue;
    }

    // 2. Perform atomic stock update
    $updateSql = "UPDATE products SET quantity = quantity + $amount WHERE name = '$name'";
    mysqli_query($conn, $updateSql);

    $affected = mysqli_affected_rows($conn);
    echo "Updated: $name, rows affected: $affected\n";
}

// Render updated table snapshot
echo "\n--- Updated Table ---\n";
$result = mysqli_query($conn, "SELECT * FROM products");
while ($row = mysqli_fetch_assoc($result)) {
    echo $row['name'] . " - " . $row['quantity'] . " in stock\n";
}
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Check Row Existence**
  `mysqli_num_rows($checkResult) === 0` checks whether any database records matched the item search name.

* **Step 2: SQL Relative Increments**
  Using `quantity = quantity + $amount` inside SQL directly avoids database race condition issues compared to calculating additions inside PHP code.

* **Step 3: Check Modification Count**
  `mysqli_affected_rows($conn)` returns exact count of database table rows altered by the latest query operation.

---

### Task 4: Delete Operations & Soft-Delete Best Practices

#### 📌 Problem Description
Build `cleanup.php` to:
1. Find and print products where `quantity = 0`.
2. Delete zero-stock products via `DELETE FROM products WHERE quantity = 0;`.
3. Print deleted count using `mysqli_affected_rows()`.
4. Include top comment block answering: *Is hard DELETE safe in production? What is a Soft Delete?*

---

#### 💻 Full Solution Code
```php
<?php
/*
  ===================================================================
  TECHNICAL DISCUSSION: HARD DELETE VS SOFT DELETE
  ===================================================================
  In production systems, HARD DELETING (DELETE FROM) rows is dangerous 
  because data is permanently removed, making recovery impossible if 
  deleted by mistake or needed for future financial/auditing reports.

  A "SOFT DELETE" uses a column like `is_deleted` (BOOLEAN) or `deleted_at` 
  (DATETIME). Instead of removing the row, we UPDATE the column:
  `UPDATE products SET is_deleted = 1 WHERE id = 5;`
  Normal SELECT queries exclude soft-deleted items (`WHERE is_deleted = 0`), 
  preserving data history safely.
  ===================================================================
*/

require_once("connect.php");

// Set one item to 0 stock for testing demonstration
mysqli_query($conn, "UPDATE products SET quantity = 0 WHERE name = 'Headphones'");

echo "--- Out of stock before delete ---\n";
$result = mysqli_query($conn, "SELECT * FROM products WHERE quantity = 0");
while ($row = mysqli_fetch_assoc($result)) {
    echo $row['name'] . "\n";
}

// Delete zero stock products
mysqli_query($conn, "DELETE FROM products WHERE quantity = 0");
echo "\nRows deleted: " . mysqli_affected_rows($conn) . "\n";

// Count remaining items
$countResult = mysqli_query($conn, "SELECT COUNT(*) AS total FROM products");
$countRow    = mysqli_fetch_assoc($countResult);
echo "Products remaining: " . $countRow['total'] . "\n";
?>
```

---

#### 🛠️ Step-by-Step Explanation

* **Step 1: Read Items Before Deletion**
  Query items matching `quantity = 0` to display items marked for removal.

* **Step 2: Hard Delete Action**
  `DELETE FROM products WHERE quantity = 0` removes those rows completely from database storage.

* **Step 3: Count Remaining Table Records**
  `SELECT COUNT(*) AS total` aggregates total remaining database rows efficiently without loading full record payloads into server memory.
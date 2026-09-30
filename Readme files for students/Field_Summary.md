# WE Student Portal – Field Training Guide (Unit 19)

Welcome to the **WE Student Portal** project repository. This guide covers the complete application code, UI components, and logic explanations for **Unit 19 (Field Training)** at WE Applied Technology Schools (WE ATS). 

---


## 🎯 Target Learning Outcomes

By completing this field training project, students demonstrate proficiency in:

* **UI & Component Design:** Reusing component blocks across dynamic web scripts using dynamic inclusions (`include`).
* **PHP Form Handling:** Processing HTTP `POST` inputs, trimming parameters, and validating values.
* **Server-Side Data Logic:** Querying datasets, running conditions, and computing pass/fail statuses dynamically.
* **Dynamic Visualization:** Rendering UI elements (badges, cards, interactive tables) based on database states.
* **CRUD Application Logic:** Implementing Creation (Add Student), Reading (Search/List Students), and Deletion procedures.

---

## 📂 Project Structure

```text
school_portal/
├── nav.php         # Global navigation header component
├── student.php     # Public Student Result Search portal
└── index.php       # Admin Management Dashboard
```

---

## 🧩 Phase 1: Navigation Component (`nav.php`)

### 📝 Code Implementation

```html
<!-- Bootstrap 5 CSS CDN -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

<nav class="navbar navbar-expand-lg navbar-dark bg-primary mb-4 shadow-sm">
  <div class="container">
    <a class="navbar-brand fw-bold" href="#">WE Student Portal</a>
    <div class="navbar-nav">
      <a class="nav-link" href="student.php">Student Check</a>
      <a class="nav-link fw-bold text-warning" href="index.php">Dashboard (Admin)</a>
    </div>
  </div>
</nav>
```

### 🔍 Code & Feature Breakdown

1. **Bootstrap CDN Integration:** Imports the Bootstrap 5 stylesheet, providing responsive grid layouts and utility classes without requiring local CSS files.
2. **Navbar Layout (`<nav>`):** Uses `navbar-expand-lg`, `navbar-dark`, and `bg-primary` to establish a dark-themed blue navigation bar aligned with school brand colors.
3. **Responsive Container (`div.container`):** Wraps header content to center-align the navbar elements cleanly across various screen breakpoints.
4. **Navigation Links:** 
   * `Student Check`: Links directly to `student.php` for students to search their grades.
   * `Dashboard (Admin)`: Styled with `text-warning` to highlight the administrator backend access (`index.php`).

---

## 🔍 Phase 2: Student Search Page (`student.php`)

### 📝 Code Implementation

```php
<?php
// Database connection
$conn = mysqli_connect("localhost", "root", "", "school_db");
if (!$conn) { 
    die("Database Connection Failed: " . mysqli_connect_error()); 
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Portal - Check Result</title>
</head>
<body class="bg-light">

    <?php include 'nav.php'; ?>

    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <!-- Search Form Card -->
                <div class="card shadow-sm p-4 mb-4 border-0">
                    <h3 class="text-primary mb-3 text-center">Find Your Result</h3>
                    <form method="POST" action="student.php">
                        <div class="mb-3">
                            <label class="form-label fw-bold">Enter Your Name:</label>
                            <input type="text" name="search_name" class="form-control form-control-lg" placeholder="e.g. Ahmed" required>
                        </div>
                        <button type="submit" class="btn btn-primary w-100 btn-lg">Search</button>
                    </form>
                </div>

                <!-- PHP Search Logic & Result Display -->
                <?php
                if ($_SERVER['REQUEST_METHOD'] == 'POST') {
                    $search_name = trim($_POST['search_name']);
                    
                    // Search database using wildcard matching
                    $search_sql = "SELECT * FROM students WHERE name LIKE '%$search_name%'";
                    $result = mysqli_query($conn, $search_sql);

                    if (mysqli_num_rows($result) > 0) {
                        while ($student = mysqli_fetch_assoc($result)) {
                            $score = $student['score'];
                            $isPass = $score >= 50;
                            $statusText = $isPass ? "Pass" : "Fail";
                            $badgeClass = $isPass ? "alert-success" : "alert-danger";
                            ?>
                            
                            <div class="card shadow p-4 text-center border-0 mb-4">
                                <h4 class="text-secondary">Official Result Card</h4>
                                <hr>
                                <h2 class="text-dark mb-3"><?= htmlspecialchars($student['name']) ?></h2>
                                <h3 class="mb-4">Score: <strong><?= $score ?></strong> / 100</h3>
                                <div class="alert <?= $badgeClass ?> fw-bold fs-4 mb-0">
                                    Status: <?= $statusText ?>
                                </div>
                            </div>

                            <?php
                        }
                    } else {
                        echo "<div class='alert alert-warning text-center fw-bold fs-5 shadow-sm'>
                                No student found matching \"" . htmlspecialchars($search_name) . "\".
                              </div>";
                    }
                }
                ?>
            </div>
        </div>
    </div>

</body>
</html>
```

### 🔍 Code & Feature Breakdown

1. **Modular Inclusions (`include 'nav.php'`):** Embeds the navigation header into the layout dynamically.
2. **Input Sanitization (`trim()` & `htmlspecialchars()`):**
   * `trim()` removes leading and trailing white spaces from student search submissions.
   * `htmlspecialchars()` encodes entity characters before rendering output, preventing Cross-Site Scripting (XSS) vulnerability issues.
3. **Wildcard Search (`LIKE '%...%'`):** Allows partial matching searches so students can locate their records even if they enter a partial first name.
4. **Automated Pass/Fail Threshold Calculation:** Evaluates `$score >= 50` to determine the status dynamically:
   * **Score $\ge$ 50:** Applies green styling (`alert-success`) with "Pass" text.
   * **Score < 50:** Applies red styling (`alert-danger`) with "Fail" text.
5. **No Results Alert:** Checks `mysqli_num_rows($result)`. If no matches exist, it alerts the user cleanly without throwing server errors.

---

## 🛠️ Phase 3: Admin Dashboard (`index.php`)

### 📝 Code Implementation

```php
<?php
// Database connection
$conn = mysqli_connect("localhost", "root", "", "school_db");
if (!$conn) { 
    die("Database Connection Failed: " . mysqli_connect_error()); 
}

// Delete Student Record Logic
if (isset($_GET['delete_id'])) {
    $delete_id = $_GET['delete_id'];
    mysqli_query($conn, "DELETE FROM students WHERE id = $delete_id");
    header("Location: index.php");
    exit();
}

// Add New Student Record Logic
if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $name = $_POST['student_name'];
    $score = $_POST['student_score'];

    if (!empty($name) && is_numeric($score)) {
        mysqli_query($conn, "INSERT INTO students (name, score) VALUES ('$name', $score)");
        header("Location: index.php");
        exit();
    }
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard - WE Student Portal</title>
</head>
<body class="bg-light">

    <?php include 'nav.php'; ?>

    <div class="container">
        <h2 class="mb-4 text-secondary">Admin Dashboard</h2>
        
        <div class="row">
            <!-- Form: Add New Student -->
            <div class="col-md-4 mb-4">
                <div class="card shadow-sm p-4 border-0">
                    <h4 class="card-title text-success mb-4">Add New Student</h4>
                    <form method="POST" action="index.php">
                        <div class="mb-3">
                            <label class="form-label fw-bold">Student Name</label>
                            <input type="text" name="student_name" class="form-control" required>
                        </div>
                        <div class="mb-4">
                            <label class="form-label fw-bold">Score</label>
                            <input type="number" name="student_score" class="form-control" required min="0" max="100">
                        </div>
                        <button type="submit" class="btn btn-success w-100">Save to Database</button>
                    </form>
                </div>
            </div>

            <!-- Table: View & Manage Student Records -->
            <div class="col-md-8">
                <div class="card shadow-sm p-4 border-0">
                    <h4 class="card-title text-primary mb-4">Full Student Records</h4>
                    <div class="table-responsive">
                        <table class="table table-hover table-striped align-middle text-center">
                            <thead class="table-dark">
                                <tr>
                                    <th>ID</th>
                                    <th>Name</th>
                                    <th>Score</th>
                                    <th>Status</th>
                                    <th>Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <?php
                                $result = mysqli_query($conn, "SELECT * FROM students");
                                while ($row = mysqli_fetch_assoc($result)):
                                    $isPass = $row['score'] >= 50; 
                                ?>
                                <tr>
                                    <td><?= $row['id'] ?></td>
                                    <td class="fw-bold"><?= htmlspecialchars($row['name']) ?></td>
                                    <td><?= $row['score'] ?></td>
                                    <td>
                                        <span class="badge <?= $isPass ? 'bg-success' : 'bg-danger' ?> px-3 py-2">
                                            <?= $isPass ? 'Pass' : 'Fail' ?>
                                        </span>
                                    </td>
                                    <td>
                                        <a href="index.php?delete_id=<?= $row['id'] ?>" 
                                           class="btn btn-sm btn-outline-danger"
                                           onclick="return confirm('Are you sure you want to delete this student?');">
                                            Delete
                                        </a>
                                    </td>
                                </tr>
                                <?php endwhile; ?>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- Portal Footer -->
        <footer class="text-center mt-5 py-3 text-muted border-top">
            <p>&copy; 2026 WE Applied Technology School - Student Portal System</p>
        </footer>
    </div>

</body>
</html>
```

### 🔍 Code & Feature Breakdown

1. **Delete Request Handler (`$_GET['delete_id']`):**
   * Detects deletion requests through URL query strings (`index.php?delete_id=X`).
   * Runs the corresponding SQL `DELETE` query and redirects back to `index.php` using `header()` redirect routines to prevent repeated execution on page refresh.
2. **Form Submission & Record Insertion (`$_POST`):**
   * Validates non-empty name inputs and numerical score inputs (`is_numeric()`).
   * Inserts records using `INSERT INTO students` queries before refreshing the dashboard view.
3. **Dynamic Data Table:**
   * Queries and iterates through every student row using `mysqli_fetch_assoc()`.
   * Formats the student pass status inside small Bootstrap badges (`bg-success` for scores $\ge$ 50, `bg-danger` for scores < 50).
4. **Client-Side Delete Confirmation (`onclick` event):**
   * Prompts a JavaScript browser confirmation box (`confirm(...)`) prior to deletion, preventing accidental record deletion.
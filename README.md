# CSV Localization Library
Localization through CSV tables.

**Links**:
- [GitHub](https://github.com/paziphik/csvlm)
- [Cargo](https://crates.io/crates/csvlm)

## Getting Started
In this walkthrough, we'll be using **Google Sheets** as a tool.
### Step 1 - Creating a Table
<img src="http://luke.guru/2iQO5XK" width=50%>

As you can see, a table with IDs in the first column, and languages in the first row should be created. This should be
relatively easy to comprehend.

### Step 2 - Save Table as **.csv**
<img src="http://luke.guru/2jF1Aqq" width=50%>

### Step 3 - Add **csvlm** as Dependency
1. In your *cargo.toml* add
```Rust
[dependencies]
// Assign latest version (Might not be the one saying)
csvlm = "0.1.3"
```
<br>
2. In the command line run
`cargo install`
<br>
<br>
3. In your executable/library of choice add
```Rust
extern crate csvlm;

use csvlm::Manager;
```

### Step 4 - Create Manager & Parse
Now we need a manager that parses the information for us
```Rust
// The parameters are directory, filename & extension
// My file is located outside of the project
let mut manag = Manager::new("..", "test_table", ".txt");

// Then parse the file assigned
manag.parse();
```

### Step 5 - Set Default Language
```Rust
// (Code continues from earlier)
// Set your default language with any available language id
m.set_def(0);
// Get language reference & vector of word references as a tuple
let (lang, word_vec) = m.get_def();
```

## Models
### Language
``` Rust
id: i32,
name: String

// Initalizer
fn new(id: i32, name: &str) -> Language { /* ... */ }
```

### Word
``` Rust
id: i32,
lang_id: i32,
val: String

// Initalizer
fn new(id: i32, lang_id: i32, val: &str) -> Word { /* ... */ }
```

### Manager
``` Rust
file: File,
langs: Vec<Language>,
words: Vec<Word>,
def_lang: i32

// Initalizer
fn new(direc: &str, name: &str, ext: &str) -> Manager { /* ... */ }

// Further methods

// Parses languages & words into manager model
fn parse() { /* ... */ }

// Sets default language by language id
fn set_def(lang_id: i32) { /* ... */ }

// Returns reference to set def. language & vector of references to words of language
fn get_def() -> (&Language, Vec<&Word>) { /* ... */ }

// Returns references to word of current language at index
fn get_word(word_id: i32) -> &Word { /* ... */ }

// Returns vector of references of words of current language at indicies
fn get_words(word_ids: Vec<i32>) -> Vec<&Word> { /* ... */ }


```

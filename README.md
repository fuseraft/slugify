# slugify 🥝

URL-safe, filename-safe, and snake_case slug generation for [Kiwi](https://github.com/fuseraft/kiwi).

## Installation

```bash
zest install fuseraft/slugify
```

## Usage

```kiwi
include ".zest/load.kiwi"

slugify::run("Hello, World!")          # → "hello-world"
slugify::run("Héllo Wörld")            # → "hello-world"
slugify::run("Fish & Chips")           # → "fish-and-chips"
slugify::run("100% pure")              # → "100-percent-pure"
slugify::run("C++ rocks")              # → "c-plus-plus-rocks"

slugify::filename("My Report.docx")   # → "my-report.docx"
slugify::filename("Photo.JPG")        # → "photo.jpg"

slugify::snake("Hello World")         # → "hello_world"

slugify::truncate("one two three four five", 14)  # → "one-two-three"
```

## API

### `slugify::run(input)`
Converts a string to a lowercase, hyphen-separated URL-safe slug.
- Transliterates accented characters (`é` → `e`, `ö` → `o`, `Æ` → `ae`, etc.)
- Expands common symbols (`&` → `and`, `@` → `at`, `%` → `percent`, `+` → `plus`)
- Replaces non-alphanumeric characters with hyphens
- Collapses consecutive separators
- Strips leading and trailing hyphens

### `slugify::filename(input)`
Slugifies a filename while preserving its extension.

```kiwi
slugify::filename("My Report (Final).docx")  # → "my-report-final.docx"
slugify::filename("my.report.final.pdf")     # → "my-report-final.pdf"
```

### `slugify::snake(input)`
Converts a string to `snake_case`.

```kiwi
slugify::snake("Hello World")   # → "hello_world"
slugify::snake("foo-bar-baz")   # → "foo_bar_baz"
```

### `slugify::truncate(input, max = 60)`
Slugifies a string and truncates it to a maximum length, trimming at a word boundary.

```kiwi
slugify::truncate("one two three four five", 14)  # → "one-two-three"
slugify::truncate("short", 60)                    # → "short"
```

## License

[MIT](https://opensource.org/licenses/MIT)

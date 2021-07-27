# Bash substring extractions
(_2021/07/27_)

Bash allows for easy (and pretty powerful) substring extractions.

---

#### Syntax:
`${<SOURCE_STRING><OPERATOR><MATCHING_PATTERN>}`

---

#### `MATCHING_PATTERN`:
Follows the usual [pattern matching](https://www.gnu.org/software/bash/manual/html_node/Pattern-Matching.html) techniques.

_E.g. `*ski` matches "Bartek Lipinski"._
<br><br>

#### `OPERATOR`:
* `#` **deletes** the _shortest_ match of `MATCHING_PATTERN` searching from the **front** of `SOURCE_STRING`.

  ```bash
  URL='https://www.youtube.com/watch?v=dQw4w9WgXcQ'
  SUBSTRING="${URL#*://}"
  # SUBSTRING is 'www.youtube.com/watch?v=dQw4w9WgXcQ'

  # removes the shortest string that matches `*://` from the front of $URL
  ```

* `##` **deletes** the _longest_ match of `MATCHING_PATTERN` searching from the **front** of `SOURCE_STRING`.

  ```bash
  URL='https://www.youtube.com/watch?v=dQw4w9WgXcQ'
  SUBSTRING="${URL##*/w}"
  # SUBSTRING is 'atch?v=dQw4w9WgXcQ'

  # removes the longest string that matches `*/w` from the front of $URL
  # if it was using '# (the shortest) the SUBSTRING would be 'ww.youtube.com/watch?v=dQw4w9WgXcQ'
  # but for the '##' SUBSTRING is 'atch?v=dQw4w9WgXcQ' because it matches the last '/w'
  ```
* `%` **deletes** the _shortest_ match of `MATCHING_PATTERN` searching from the **end** of `SOURCE_STRING`.
* `%%` **deletes** the _longest_ match of `MATCHING_PATTERN` searching from the **end** of `SOURCE_STRING`.

## TL;DR:

[1](#1) Allow finding an `issue` / `PR` by the labels it has WITHOUT prefixing the search string with "`label:`"

AND/OR

[2](#2) provide a shorter syntax to filter with labels, such as "`:priority:high`" or "`priority:high:`" as "`label:priority:high`".

AND/OR

[3](#3) provide a separate field specifically for filtering with labels (something that extensions like [Refined GitHub](https://github.com/sindresorhus/refined-github) could create?)

# Explanation

I've set-up a sample repo for a better explanation @ https://github.com/sarpik/github-filter-by-label-example

## data

example label name: `priority:high` (https://github.com/sarpik/github-filter-by-label-example/labels/priority%3Ahigh)

example issue's data (irrelevant properties removed, except `labels` - everything is kept):

```sh
curl -i "https://api.github.com/repos/sarpik/github-filter-by-label-example/issues/1"
```

```json
{
  "title": "Sample issue",
  "body": "Sample description",
  "labels": [
    {
      "id": 1520443741,
      "node_id": "MDU6TGFiZWwxNTIwNDQzNzQx",
      "url": "https://api.github.com/repos/sarpik/github-filter-by-label-example/labels/priority:high",
      "name": "priority:high",
      "color": "b50125",
      "default": false
    }
  ],
}
```

## Current behavior

When the search string is "`priority:high`"
(https://github.com/sarpik/github-filter-by-label-example/issues?utf8=%E2%9C%93&q=priority%3Ahigh),

the issue IS NOT found.

If the search string is prefixed with "`label:`" (equal to "`label:priority:high`" (https://github.com/sarpik/github-filter-by-label-example/issues?utf8=%E2%9C%93&q=label%3Apriority%3Ahigh)),

the issue IS found.

## Desired behavior

The issue IS found in BOTH cases.

### Note

If the `body` / `title` contained "`priority:high`", then the issue WOULD have been found in BOTH cases.

## Possible solutions

### 1

Would it be possible to make each label's `name` act the same way as `body` or `title` when searching / filtering, so that the desired effect would be achieved?

Drawbacks:

* Issues containing text "`priority:high`" but without an actual "`priority:high`" label could get in the way, which may or may not be desired

### 2

Allow users to use a shorter syntax for searching with labels:

Instead of using "`label:priority:high`", one could use a shorter syntax, which would still limit the search to labels only, but would be easier and/or shorter to type.

Shorthand syntax ideas:

* a single colon `:`, followed by the label name:

"`:priority:high`" as "`label:priority:high`"

* the opposite - the label name, followed by a single colon `:`:

"`priority:high:`" as "`label:priority:high`"

note that with this solution it would be easier to remove the colon and then search without a limitation to labels-only.

Drawbacks:

None that I can think of -- although, maybe use an an opt-in?

### 3

Just provide a separate field specifically for filtering with labels (something that extensions like [Refined GitHub](https://github.com/sindresorhus/refined-github) could create?)

Also as an opt-in?

---

## Originally

I have some labels like `priority:high`, `priority:medium`, `priority:low`.

If I want to search for issues with these labels, I have to type `label:priority:some_priority`.

I'd love to be able to use either of the [solutions]() mentioned above, because it'd be faster and more comfortable to type, thus saving time & energy.

This is not only for `priority:` - labels such as, but not limited to, `scope:`, `type:`, `status:`, `resolution:`, `difficulty:`, `component:` etc. - whatevery way you want to categorize - would also be useful.

## See also

https://github.com/sarpik/github-filter-by-label-example

https://help.github.com/en/articles/searching-issues-and-pull-requests#search-by-label

https://help.github.com/en/articles/filtering-issues-and-pull-requests-by-labels

https://help.github.com/en/articles/keyboard-shortcuts#issue-and-pull-request-lists

https://github.com/search/advanced

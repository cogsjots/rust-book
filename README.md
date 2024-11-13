
This repository contains the html version for Rust 1.82.0 (released 2024-10-17).
Please use the main [rust-book](https://github.com/rust-lang/book) repository to get latest version.

This branch is used to create a print version from print.html.

It uses the following script to first clean out unnecssary lines in html files:

```sh
delete_lines() {
    local file="$1"
    # local start="$2"
    # local end="$3"

    lines=$(wc -l < "$file")
    if [ $lines -gt 175 ]; then
        start=$((lines - $2))
        end=$((lines - $3))
        sed -i "$start,$end d" "$file"
    fi
}

for file in *.html; do

    lines=$(wc -l < "$file")
    if [ $lines -gt 175 ]; then
        # Delete lines 35 to 26
        delete_lines "$file" 34 26

        # Delete lines 50 to 39
        delete_lines "$file" 40 29
    fi

    sed -i '127,179d' "$file"
    sed -i '40,122d' "$file"
    sed -i '28,29d' "$file"
done
```

You may beed to adjust some lines it it as fro print.html it is off by 1

Other steps are :
1. Add the cover page html
2. Remove page-break before h2 tags except those for appendix.
3. update general.css and print.css.


### Search and Replace

The following are some of the parts which are replaced:

1. `a href="ch`
2. `a href="ap`
3. `<div style="break-before: page; page-break-before: always;"></div><h2` - for all h2 except in appendix sections
4. `pre><pre class="playground"><code`
5. `a href="..`

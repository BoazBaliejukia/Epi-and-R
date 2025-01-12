This template demonstrates many of the bells and whistles of the `reprex::reprex_document()` output format. The YAML sets many options to non-default values, such as using `#;-)` as the comment in front of output.

## Code style

Since `style` is `TRUE`, this difficult-to-read code (look at the `.Rmd` source file) will be restyled according to the Tidyverse style guide when it’s rendered. Whitespace rationing is not in effect!

``` r
x=1;y=2;z=x+y;z
#;-) [1] 3
```

## Quiet tidyverse

The tidyverse meta-package is quite chatty at startup, which can be very useful in exploratory, interactive work. It is often less useful in a reprex, so by default, we suppress this.

However, when `tidyverse_quiet` is `FALSE`, the rendered result will include a tidyverse startup message about package versions and function masking.

``` r
library(tidyverse)
#;-) ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
#;-) ✔ dplyr     1.1.4     ✔ readr     2.1.5
#;-) ✔ forcats   1.0.0     ✔ stringr   1.5.1
#;-) ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
#;-) ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
#;-) ✔ purrr     1.0.2     
#;-) ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
#;-) ✖ dplyr::filter() masks stats::filter()
#;-) ✖ dplyr::lag()    masks stats::lag()
#;-) ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

## Chunks in languages other than R

Remember: knitr supports many other languages than R, so you can reprex bits of code in Python, Ruby, Julia, C++, SQL, and more. Note that, in many cases, this still requires that you have the relevant external interpreter installed.

Let’s try Python!

``` python
x = 'hello, python world!'
print(x.split(' '))
```

And bash!

``` bash
echo "Hello Bash!";
pwd;
ls | head;
#;-) Hello Bash!
#;-) /Users/boazbaliejukia/Documents/GitHub/Epi and R/Evans cohort
#;-) Evans cohort.Rproj
#;-) Untitled.Rmd
#;-) Untitled_reprex.Rmd
#;-) Untitled_reprex_std_out_err.txt
#;-) evans.csv
```

Write a function in C++, use Rcpp to wrap it and …

``` cpp
#include <Rcpp.h>
using namespace Rcpp;

// [[Rcpp::export]]
NumericVector timesTwo(NumericVector x) {
  return x * 2;
}
```

then immediately call your C++ function from R!

``` r
timesTwo(1:4)
#;-) [1] 2 4 6 8
```

## Standard output and error

Some output that you see in an interactive session is not actually captured by rmarkdown, when that same code is executed in the context of an `.Rmd` document. When `std_out_err` is `TRUE`, `reprex::reprex_render()` uses a feature of `callr:r()` to capture such output and then injects it into the rendered result.

Look for this output in a special section of the rendered document (and notice that it does not appear right here).

``` r
system2("echo", args = "Output that would normally be lost")
```

## Session info

Because `session_info` is `TRUE`, the rendered result includes session info, even though no such code is included here in the source document.

<details style="margin-bottom:10px;">
<summary>
Standard output and standard error
</summary>

``` sh
✖ Install the styler package in order to use `style = TRUE`.
running: bash  -c 'echo "Hello Bash!";
pwd;
ls | head;'
Building shared library for Rcpp code chunk...
Output that would normally be lost
```

</details>
<details style="margin-bottom:10px;">
<summary>
Session info
</summary>

``` r
sessioninfo::session_info()
#;-) ─ Session info ───────────────────────────────────────────────────────────────
#;-)  setting  value
#;-)  version  R version 4.4.1 (2024-06-14)
#;-)  os       macOS Ventura 13.7.2
#;-)  system   x86_64, darwin20
#;-)  ui       X11
#;-)  language (EN)
#;-)  collate  en_US.UTF-8
#;-)  ctype    en_US.UTF-8
#;-)  tz       Europe/London
#;-)  date     2024-12-24
#;-)  pandoc   3.2 @ /Applications/RStudio.app/Contents/Resources/app/quarto/bin/tools/x86_64/ (via rmarkdown)
#;-) 
#;-) ─ Packages ───────────────────────────────────────────────────────────────────
#;-)  package     * version date (UTC) lib source
#;-)  cli           3.6.3   2024-06-21 [1] CRAN (R 4.4.0)
#;-)  colorspace    2.1-0   2023-01-23 [1] CRAN (R 4.4.0)
#;-)  digest        0.6.37  2024-08-19 [1] CRAN (R 4.4.1)
#;-)  dplyr       * 1.1.4   2023-11-17 [1] CRAN (R 4.4.0)
#;-)  evaluate      1.0.1   2024-10-10 [1] CRAN (R 4.4.1)
#;-)  fansi         1.0.6   2023-12-08 [1] CRAN (R 4.4.0)
#;-)  fastmap       1.2.0   2024-05-15 [1] CRAN (R 4.4.0)
#;-)  forcats     * 1.0.0   2023-01-29 [1] CRAN (R 4.4.0)
#;-)  fs            1.6.5   2024-10-30 [1] CRAN (R 4.4.1)
#;-)  generics      0.1.3   2022-07-05 [1] CRAN (R 4.4.0)
#;-)  ggplot2     * 3.5.1   2024-04-23 [1] CRAN (R 4.4.0)
#;-)  glue          1.8.0   2024-09-30 [1] CRAN (R 4.4.1)
#;-)  gtable        0.3.5   2024-04-22 [1] CRAN (R 4.4.0)
#;-)  hms           1.1.3   2023-03-21 [1] CRAN (R 4.4.0)
#;-)  htmltools     0.5.8.1 2024-04-04 [1] CRAN (R 4.4.0)
#;-)  knitr         1.49    2024-11-08 [1] CRAN (R 4.4.1)
#;-)  lifecycle     1.0.4   2023-11-07 [1] CRAN (R 4.4.0)
#;-)  lubridate   * 1.9.3   2023-09-27 [1] CRAN (R 4.4.0)
#;-)  magrittr      2.0.3   2022-03-30 [1] CRAN (R 4.4.0)
#;-)  munsell       0.5.1   2024-04-01 [1] CRAN (R 4.4.0)
#;-)  pillar        1.9.0   2023-03-22 [1] CRAN (R 4.4.0)
#;-)  pkgconfig     2.0.3   2019-09-22 [1] CRAN (R 4.4.0)
#;-)  purrr       * 1.0.2   2023-08-10 [1] CRAN (R 4.4.0)
#;-)  R6            2.5.1   2021-08-19 [1] CRAN (R 4.4.0)
#;-)  Rcpp          1.0.12  2024-01-09 [1] CRAN (R 4.4.0)
#;-)  readr       * 2.1.5   2024-01-10 [1] CRAN (R 4.4.0)
#;-)  reprex        2.1.0   2024-01-11 [1] CRAN (R 4.4.0)
#;-)  rlang         1.1.4   2024-06-04 [1] CRAN (R 4.4.0)
#;-)  rmarkdown     2.29    2024-11-04 [1] CRAN (R 4.4.1)
#;-)  rstudioapi    0.16.0  2024-03-24 [1] CRAN (R 4.4.0)
#;-)  scales        1.3.0   2023-11-28 [1] CRAN (R 4.4.0)
#;-)  sessioninfo   1.2.2   2021-12-06 [1] CRAN (R 4.4.0)
#;-)  stringi       1.8.4   2024-05-06 [1] CRAN (R 4.4.0)
#;-)  stringr     * 1.5.1   2023-11-14 [1] CRAN (R 4.4.0)
#;-)  tibble      * 3.2.1   2023-03-20 [1] CRAN (R 4.4.0)
#;-)  tidyr       * 1.3.1   2024-01-24 [1] CRAN (R 4.4.0)
#;-)  tidyselect    1.2.1   2024-03-11 [1] CRAN (R 4.4.0)
#;-)  tidyverse   * 2.0.0   2023-02-22 [1] CRAN (R 4.4.0)
#;-)  timechange    0.3.0   2024-01-18 [1] CRAN (R 4.4.0)
#;-)  tzdb          0.4.0   2023-05-12 [1] CRAN (R 4.4.0)
#;-)  utf8          1.2.4   2023-10-22 [1] CRAN (R 4.4.0)
#;-)  vctrs         0.6.5   2023-12-01 [1] CRAN (R 4.4.0)
#;-)  withr         3.0.2   2024-10-28 [1] CRAN (R 4.4.1)
#;-)  xfun          0.49    2024-10-31 [1] CRAN (R 4.4.1)
#;-)  yaml          2.3.10  2024-07-26 [1] CRAN (R 4.4.0)
#;-) 
#;-)  [1] /Library/Frameworks/R.framework/Versions/4.4-x86_64/Resources/library
#;-) 
#;-) ──────────────────────────────────────────────────────────────────────────────
```

</details>

<!-- README.md is generated from README.Rmd. Please edit that file -->

# wellpad

## Installation

``` r
devtools::install_github("R-S-C/wellpad")
```
## Usage

Must have columns named `xs`, `ys`, `xb`, and `yb` in a a `data.frame`. These should be latitude (y)
and longitude (x) coordinates for the surface (s) and bottom-hole (b) locations in WGS84
[(EPSG:4326)](https://spatialreference.org/ref/epsg/wgs-84/). You can include any number of
additional columns in the data.frame, and these columns will be preserved in the output (e.g.,
`well_names`, `first_production_date`, etc.).

``` r
input_data <- data.frame(xs = c(-98.06853, -98.06853, -98.06853, -98.06853),
                         ys = c(28.75656, 28.75648, 28.7564, 28.75631),
                         xb = c(-98.05691, -98.05689, -98.05686, -98.05683),
                         yb = c(28.74631, 28.74465, 28.74299, 28.74133))

```

Use the collateWHT function to find groups of wells (PAD's), and calculate spacing between wells
within the same PAD. The `dist` parameter specifies the maximum distance (ft.) for a group of suface
locations to be considered as belonging to the same PAD. The example below turns out to be one PAD,
but the function will determine which wells belong to a PAD on its own and will number each pad to
identify the wells which belong to it. The hiearchy is `pad >> branch >> stem`. Individual wells are
stems, while the branch designation allows for cases where groups of wells radiate out in two
opposite directions (i.e., a pad with two branches).

``` r
library(wellpad)
collated_wells <- collateWHT(input_data, dist = 250)
```

Show the results on a map

``` r
mapIt(collated_wells)
```

## Getting help

See package documentation: `?wellpad::collateWHT` or `?wellpad::mapIt`. If you encounter a bug,
please file a minimal reproducible example on [github](https://github.com/R-S-C/wellpad/issues).

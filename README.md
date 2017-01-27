# gdxtools

The gdxtools package converts data (parameter or variables) from a GDX file (produced by the GAMS software) into a data.frame. It also provides a function to get information on a GDX file. This package is based on the R interface provided by GAMS software [gdxrrw](http://support.gams.com/doku.php?id=gdxrrw:interfacing_gams_and_r)

## Installation

Download the latest release zip here [https://github.com/lolow/gdxtools/releases/latest]

```R
install.packages("gdxtools_0.4.x.zip",repos=NULL)
```

or install the development version

```R
library("devtools")
install_github('lolow/gdxtools')
```

An interesting script can be used to load (and install if necessary) R packages, along with a function to load and install on the fly the gdxtools and its dependencies in a function __require_gdxtools__ ([see get_libraries.R](https://gist.github.com/lolow/07992971b81a156ba1f0db1b2dba9dc2))

## Usage

```R
library(gdxtools)

# If necessary, tell where is located GAMS.
igdx(dirname(Sys.which('gams'))) 

# define a gdx
> mygdx <- gdx('results.gdx')

# get information on a gdx
> print(mygdx)
<results.gdx, 8 symbols>
> print(mygdx$parameters$name)
[1] param1 param2

# get information on all items in the gdx
> all_items(mygdx)

# create a data.frame from a parameter
> travel_cost <- mygdx["travel_cost"]

# create a data.frame from the lower bound of a variable
> lo_travel_time <- mygdx["travel_time", field="lo"]

# create a data.frame from the marginal value of an equation
> m_time_constraint <- mygdx["time_constraint", field="m"]

# Extract a list of items from many GDX
> myfiles = c("test1.gdx","test2.gdx")
> allparam = batch_extract("myparam",files=myfiles)

# write gdx
> param1 = data.frame(x=c('1','2'),value=1:10)
> attributes(param1) = c(attributes(param1), gams="definition of parameter 1")
> param2 = data.frame(a=c('london','paris','tahiti'),value=c(50,0.2,1e-2))
> write.gdx("test.gdx",list(param1=param1,param2=param2))


```

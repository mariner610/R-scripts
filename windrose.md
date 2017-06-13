Windrose(ggplot..)
========================================================
author: OH, JUNH HEE
date: 2017. 06. 13
autosize: true


1. Data Loading
========================================================


```r
library(readxl)
kumos <- read_excel("./kumos_.xlsx")
str(kumos)
```

```
Classes 'tbl_df', 'tbl' and 'data.frame':	26876 obs. of  28 variables:
 $ Cruise_ID    : chr  "HI-16-01" "HI-16-01" "HI-16-01" "HI-16-01" ...
 $ Year         : num  2016 2016 2016 2016 2016 ...
 $ Month        : num  8 8 8 8 8 8 8 8 8 8 ...
 $ Day          : num  5 5 5 5 5 5 5 5 5 5 ...
 $ Hour         : num  5 5 5 5 5 5 5 5 5 5 ...
 $ Min          : num  17 19 20 21 22 23 24 25 27 28 ...
 $ SEC          : num  59 59 59 59 59 59 59 59 59 59 ...
 $ Latitude     : num  35 35 35 35 35 ...
 $ Lat_hem      : chr  "N" "N" "N" "N" ...
 $ Longitude    : num  129 129 129 129 129 ...
 $ Longitude_hem: chr  "E" "E" "E" "E" ...
 $ Course       : num  275.47 19.43 12.16 7.75 8.6 ...
 $ Speed        : num  2.1 0.2 1.7 1.8 1.9 3 4 5.9 7.8 7.7 ...
 $ Heading      : num  93.1 40.3 15.4 13.1 14.7 ...
 $ App_WS       : num  1.73 3.27 5.09 3.99 3.85 ...
 $ App_WD       : num  355.2 22.3 47.1 77.8 49.3 ...
 $ True_WS      : num  1.72 3.26 4.92 3.96 3.35 ...
 $ True_WD      : num  101.3 91.2 86.8 106.5 76.2 ...
 $ Air_Temp     : num  29.1 29.3 29.4 29.4 29.4 ...
 $ Atmos_Press  : num  1008 1008 1008 1008 1007 ...
 $ Humidity     : num  69 69.4 69.9 68.7 68.8 ...
 $ Solar_R      : num  NA NA 696 NA 820 ...
 $ Conductivity : num  48.5 48.5 48.5 48.5 48.5 ...
 $ Seawater_T1  : num  NA NA NA NA NA NA NA NA NA NA ...
 $ Seawater_T2  : num  24.1 24.1 24.1 24.1 24.1 ...
 $ Salinity     : num  NA NA NA NA NA NA NA NA NA NA ...
 $ Depth        : num  NA 4.62 4.44 4.26 4.58 5.11 5.08 5.49 NA NA ...
 $ Datetime     : POSIXct, format: NA NA ...
```

```r
kumos$Cruise_ID <- factor(kumos$Cruise_ID)
str(kumos)
```

```
Classes 'tbl_df', 'tbl' and 'data.frame':	26876 obs. of  28 variables:
 $ Cruise_ID    : Factor w/ 5 levels "HI-16-00","HI-16-01",..: 2 2 2 2 2 2 2 2 2 2 ...
 $ Year         : num  2016 2016 2016 2016 2016 ...
 $ Month        : num  8 8 8 8 8 8 8 8 8 8 ...
 $ Day          : num  5 5 5 5 5 5 5 5 5 5 ...
 $ Hour         : num  5 5 5 5 5 5 5 5 5 5 ...
 $ Min          : num  17 19 20 21 22 23 24 25 27 28 ...
 $ SEC          : num  59 59 59 59 59 59 59 59 59 59 ...
 $ Latitude     : num  35 35 35 35 35 ...
 $ Lat_hem      : chr  "N" "N" "N" "N" ...
 $ Longitude    : num  129 129 129 129 129 ...
 $ Longitude_hem: chr  "E" "E" "E" "E" ...
 $ Course       : num  275.47 19.43 12.16 7.75 8.6 ...
 $ Speed        : num  2.1 0.2 1.7 1.8 1.9 3 4 5.9 7.8 7.7 ...
 $ Heading      : num  93.1 40.3 15.4 13.1 14.7 ...
 $ App_WS       : num  1.73 3.27 5.09 3.99 3.85 ...
 $ App_WD       : num  355.2 22.3 47.1 77.8 49.3 ...
 $ True_WS      : num  1.72 3.26 4.92 3.96 3.35 ...
 $ True_WD      : num  101.3 91.2 86.8 106.5 76.2 ...
 $ Air_Temp     : num  29.1 29.3 29.4 29.4 29.4 ...
 $ Atmos_Press  : num  1008 1008 1008 1008 1007 ...
 $ Humidity     : num  69 69.4 69.9 68.7 68.8 ...
 $ Solar_R      : num  NA NA 696 NA 820 ...
 $ Conductivity : num  48.5 48.5 48.5 48.5 48.5 ...
 $ Seawater_T1  : num  NA NA NA NA NA NA NA NA NA NA ...
 $ Seawater_T2  : num  24.1 24.1 24.1 24.1 24.1 ...
 $ Salinity     : num  NA NA NA NA NA NA NA NA NA NA ...
 $ Depth        : num  NA 4.62 4.44 4.26 4.58 5.11 5.08 5.49 NA NA ...
 $ Datetime     : POSIXct, format: NA NA ...
```

```r
dim(kumos)
```

```
[1] 26876    28
```

2. Extraction data..
========================================================

```r
hangcha <- kumos[,1]
Month <- kumos[,3]
Hour <- kumos[,5]
spd <- kumos[,17]
dir <- kumos[,18]
df <- data.frame(hangcha, Month, Hour, spd, dir)
names(df)[1]<-"hangcha"
str(df)
```

```
'data.frame':	26876 obs. of  5 variables:
 $ hangcha: Factor w/ 5 levels "HI-16-00","HI-16-01",..: 2 2 2 2 2 2 2 2 2 2 ...
 $ Month  : num  8 8 8 8 8 8 8 8 8 8 ...
 $ Hour   : num  5 5 5 5 5 5 5 5 5 5 ...
 $ spd    : num  1.72 3.26 4.92 3.96 3.35 ...
 $ dir    : num  101.3 91.2 86.8 106.5 76.2 ...
```

```r
head(df)
```

```
   hangcha Month Hour      spd       dir
1 HI-16-01     8    5 1.723796 101.30310
2 HI-16-01     8    5 3.256355  91.23310
3 HI-16-01     8    5 4.920528  86.76074
4 HI-16-01     8    5 3.963347 106.45040
5 HI-16-01     8    5 3.349347  76.16217
6 HI-16-01     8    5 4.109369 101.18940
```

3. Windrose Function..

```r
# WindRose.R
require(ggplot2)
require(RColorBrewer)

plot.windrose <- function(data,
                      spd,
                      dir,
                      spdres = 2,
                      dirres = 30,
                      spdmin = 2,
                      spdmax = 20,
                      spdseq = NULL,
                      palette = "YlGnBu",
                      countmax = NA,
                      debug = 0){


# Look to see what data was passed in to the function
  if (is.numeric(spd) & is.numeric(dir)){
    # assume that we've been given vectors of the speed and direction vectors
    data <- data.frame(spd = spd,
                       dir = dir)
    spd = "spd"
    dir = "dir"
  } else if (exists("data")){
    # Assume that we've been given a data frame, and the name of the speed 
    # and direction columns. This is the format we want for later use.    
  }  

  # Tidy up input data ----
  n.in <- NROW(data)
  dnu <- (is.na(data[[spd]]) | is.na(data[[dir]]))
  data[[spd]][dnu] <- NA
  data[[dir]][dnu] <- NA

  # figure out the wind speed bins ----
  if (missing(spdseq)){
    spdseq <- seq(spdmin,spdmax,spdres)
  } else {
    if (debug >0){
      cat("Using custom speed bins \n")
    }
  }
  # get some information about the number of bins, etc.
  n.spd.seq <- length(spdseq)
  n.colors.in.range <- n.spd.seq - 1

  # create the color map
  spd.colors <- colorRampPalette(brewer.pal(min(max(3,
                                                    n.colors.in.range),
                                                min(9,
                                                    n.colors.in.range)),                                               
                                            palette))(n.colors.in.range)

  if (max(data[[spd]],na.rm = TRUE) > spdmax){    
    spd.breaks <- c(spdseq,
                    max(data[[spd]],na.rm = TRUE))
    spd.labels <- c(paste(c(spdseq[1:n.spd.seq-1]),
                          '-',
                          c(spdseq[2:n.spd.seq])),
                    paste(spdmax,
                          "-",
                          max(data[[spd]],na.rm = TRUE)))
    spd.colors <- c(spd.colors, "grey50")
  } else{
    spd.breaks <- spdseq
    spd.labels <- paste(c(spdseq[1:n.spd.seq-1]),
                        '-',
                        c(spdseq[2:n.spd.seq]))    
  }
  data$spd.binned <- cut(x = data[[spd]],
                         breaks = spd.breaks,
                         labels = spd.labels,
                         ordered_result = TRUE)
  # clean up the data
  data. <- na.omit(data)

  # figure out the wind direction bins
  dir.breaks <- c(-dirres/2,
                  seq(dirres/2, 360-dirres/2, by = dirres),
                  360+dirres/2)  
  dir.labels <- c(paste(360-dirres/2,"-",dirres/2),
                  paste(seq(dirres/2, 360-3*dirres/2, by = dirres),
                        "-",
                        seq(3*dirres/2, 360-dirres/2, by = dirres)),
                  paste(360-dirres/2,"-",dirres/2))
  # assign each wind direction to a bin
  dir.binned <- cut(data[[dir]],
                    breaks = dir.breaks,
                    ordered_result = TRUE)
  levels(dir.binned) <- dir.labels
  data$dir.binned <- dir.binned

  # Run debug if required ----
  if (debug>0){    
    cat(dir.breaks,"\n")
    cat(dir.labels,"\n")
    cat(levels(dir.binned),"\n")       
  }  

  # deal with change in ordering introduced somewhere around version 2.2
  if(packageVersion("ggplot2") > "2.2"){    
    cat("Hadley broke my code\n")
    data$spd.binned = with(data, factor(spd.binned, levels = rev(levels(spd.binned))))
    spd.colors = rev(spd.colors)
  }

  # create the plot ----
  p.windrose <- ggplot(data = data,
                       aes(x = dir.binned,
                           fill = spd.binned)) +
    geom_bar() + 
    scale_x_discrete(drop = FALSE,
                     labels = waiver()) +
    coord_polar(start = -((dirres/2)/360) * 2*pi) +
    scale_fill_manual(name = "Wind Speed (m/s)", 
                      values = spd.colors,
                      drop = FALSE) +
    #theme_bw() +
    theme(axis.title.x = element_blank(),
          #panel.border = element_rect(colour = "blank"),
          panel.grid.major = element_line(colour="grey65"))

  # adjust axes if required
  if (!is.na(countmax)){
    p.windrose <- p.windrose +
      ylim(c(0,countmax))
  }

  # print the plot
  print(p.windrose)  

  # return the handle to the wind rose
  return(p.windrose)
}
```











```
Error in NROW(data) : 기본값이 없는 인수 "data"가 누락되어 있습니다
```

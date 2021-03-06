# pyPRISMClimate

An interface to the PRISM Climate data with functions similar
to the R package [prism](https://github.com/ropensci/prism)


- [Installation](#installation)
- [Quick Start](#quick-start)
- [API](#api)
  - [pyPRISMClimate.get_prism_dailys()](#pyprismclimateget_prism_dailys)
  - [pyPRISMClimate.get_prism_daily_single()](#pyprismclimateget_prism_daily_single)
  - [pyPRISMClimate.get_prism_monthlys()](#pyprismclimateget_prism_monthlys)
  - [pyPRISMClimate.get_prism_monthly_single()](#pyprismclimateget_prism_monthly_single)
- [Acknowledgments](#acknowledgments)

## Installation

Requires python 3. No other packages needed.

```
pip install git+git://github.com/sdtaylor/pyPRISMClimate
```

## Quick Start

Four primary functions are available to get a single date, or series of dates,
of either the daily or monthly prism data.

Available variables are tmean, tmin, tmax, or ppt.

```
from pyPRISMClimate import get_prism_monthlys, get_prism_monthly_single, get_prism_dailys, get_prism_daily_single

# Get monthly mean temperature
get_prism_monthlys(variable='tmean', years=[2017,2018], months=[1,2,3,4], dest_path='/tmp/prism')

# Get a single monthly temperature file and return path of the final bil file
may_2017_tmin = get_prism_monthly_single(variable='tmin', year=2017, month=5, return_path=True)
may_2017_tmin 
> '/tmp/p/PRISM_tmin_stable_4kmM2_201705_bil.bil'

# Get daily maximum temperature for Jan. 1, 2017 to Feb. 20, 2017
get_prism_dailys('tmax',min_date='2017-01-01', max_date='2017-02-01', dest_path='/tmp/p/')

# Get the daily minimum temperature for July 1, 2005
get_prism_daily_single('tmax', '2005-07-07')

```

## API

##### pyPRISMClimate.get_prism_dailys()

    get_prism_dailys(variable,
                     min_date,
                     max_date,
                     dates=None,
                     dest_path='./',
                     keep_zip=True)
    Downlaod PRISM Daily data

    Parameters:
        variable : str
            Either tmean, tmax, tmin, or ppt
        
        min_date : str
            Start date to download in the format YYYY-MM-DD
        
        max_date : str
            End date to download in the format YYYY-MM-DD. Note min and max
            are inclusive. 
            
        dates : list of python datetimes, optional
            Specific dates to download, should be a list of python datetimes.           
            years and months parameters are ignored if this is set. 
        
        dest_path : str, optional
            Folder to download to, defaults to the current working directory.
        
        keep_zip : bool, optional
            Keeps the originally downloaded zip files, default True
            
##### pyPRISMClimate.get_prism_daily_single()

    get_prism_daily_single(variable,
                           date,
                           dest_path='./',
                           return_path=False,
                           keep_zip=True)
    Download data for a single day
    
    Parameters:
        variable : str
            Either tmean, tmax, tmin, or ppt
        
        date : str
            The date to download in the format YYYY-MM-DD
        
        dest_path : str, optional
            Folder to download to, defaults to the current working directory.
    
        return_path : bool, optional
            Returns the full path to the final bil file, default False
        
        keep_zip : bool, optional
            Keeps the originally downloaded zip file, default True
            
#### pyPRISMClimate.get_prism_monthlys()

    get_prism_monthlys(variable,
                       years,
                       months,
                       dates=None,
                       dest_path='./',
                       keep_zip=True)
                       
    Download monthly PRISM data
    
    Parameters:
        variable : str
            Either tmean, tmax, tmin, or ppt
        
        years : list of integers
            The years to download
        
        months : list of integers
            The months to download
            
        dates : list of python datetimes, optional
            Specific months to download, should be a list of python datetimes.
            The day for each date should be set to the 1st            
            years and months parameters are ignored if this is set. 
        
        dest_path : str, optional
            Folder to download to, defaults to the current working directory.
        
        keep_zip : bool, optional
            Keeps the originally downloaded zip files, default True


#### pyPRISMClimate.get_prism_monthly_single()

    get_prism_monthly_single(variable,
                             year,
                             month,
                             date=None,
                             dest_path='./',
                             return_path=False,
                             keep_zip=True)
                             
    Download data for a single day
    
    Parameters:
        variable : str
            Either tmean, tmax, tmin, or ppt
        
        year : int
            The year to download
        
        month : int
            The month to download
        
        date : str, optional
            The date to download as a python datetime. The day should
            be set to 01. If set than year and month are ignored.
        
        dest_path : str, optional
            Folder to download to, defaults to the current working directory.
    
        return_path : bool, optional
            Returns the full path to the final bil file, default False
        
        keep_zip : bool, optional
            Keeps the originally downloaded zip file, default True
            
        
## Acknowledgments

Development of this software was funded by
[the Gordon and Betty Moore Foundation's Data-Driven Discovery Initiative](http://www.moore.org/programs/science/data-driven-discovery) through
[Grant GBMF4563](http://www.moore.org/grants/list/GBMF4563) to Ethan P. White.

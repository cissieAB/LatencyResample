# Latency Statistics

This is a project to automatically calculate the monthly and yearly *success rates* based on the day-to-day latency input 
Excel files. 

## Environment
This project is developed with Python3, Python Pandas module and Jupyter Notebook. 
Please make sure you have all the related packages installed. 
Or, I personally recommend installing the popular [Anaconda](https://www.anaconda.com/) to run the scripts. 

## Usage
### Inputs
The 6 input Excel files are located in `/input_excel_files/`. 
You may click [here](./input_excel_files/Aqua_Version3C_dates.xlsx) to read a sample input.

For each Excel file, please following the naming rules as `tsr_vstr_dates.xlsx`, 
where `tsr` is in `Aqua`, `Terra` and `TISA`, and `vstr` is in `Version3C` and `Version4A`. 
*The file names are hard coded in the scripts.*
If you want to change the names, please also change their appearances in the code.

### Outputs
The output files are all csv files.
The monthly success rate files are at [`./results/monthly`](`./results/monthly`), and the 
yearly ones are at [`./results/annually`](`./results/annually`). These locations and file 
names are also hard-coded in scripts.

### Running the scripts
1. Run [`get_monthly_suc_rates_statistics.ipynb`](./get_monthly_suc_rates_statistics.ipynb) first to
get the monthly statistics.
2. Then run [`get_annual_suc_rates_statistics.ipynb`](./get_annual_suc_rates_statistics.ipynb) to get the annual
statistics.

### Configuring target delays
Currently, for Aqua/Terra SSF products, the target of the delay is within 3/4 days. 
For TISA products, the target of the delay is within 6/7 days.

If the target is changed, please set the parameters in the `TargetDelay` class defined in 
`get_monthly_suc_rates_statistics.ipynb`
to the updated values.

```python
# target delay constants
class TargetDelay:
    def __init__(self, type_str):
        if type_str == TISA:
            # the 1st target of TISA, change this when the target is setting to other value
            self.delay_1 = timedelta(6)
            self.delay_1_name = 'Flag_delay_in_6_days'
            # 2nd target of TISA
            self.delay_2 = timedelta(7)
            self.delay_2_name = 'Flag_delay_in_7_days'
        elif type_str in [AQUA, TERRA]:
            # 1st target of the SSF products
            self.delay_1 = timedelta(3)
            self.delay_1_name = 'Flag_delay_in_3_days'
            # 2nd target of the SSF products
            self.delay_2 = timedelta(4)
            self.delay_2_name = 'Flag_delay_in_4_days'
```


## References
- [Resample time series in Pandas](https://www.geeksforgeeks.org/python-pandas-dataframe-resample/)

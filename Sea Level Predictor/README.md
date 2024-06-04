# The Needed Function
```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress
import numpy as np

def draw_plot():
    # Read data from file
    df = pd.read_csv('epa-sea-level.csv')

    # Create scatter plot
    plt.scatter(df['Year'], df['CSIRO Adjusted Sea Level'])

    # Create first line of best fit
    slope, intercept, r_value, p_value, std_err = linregress(df['Year'], df['CSIRO Adjusted Sea Level'])
    years_extended = np.arange(df['Year'].min(), 2051)
    plt.plot(years_extended, intercept + slope * years_extended, 'r', label='Best Fit Line 1')

    # Create second line of best fit
    recent_years = df[df['Year'] >= 2000]
    recent_slope, recent_intercept, _, _, _ = linregress(recent_years['Year'], recent_years['CSIRO Adjusted Sea Level'])
    recent_years_extended = np.arange(2000, 2051)
    plt.plot(recent_years_extended, recent_intercept + recent_slope * recent_years_extended, 'b', label='Best Fit Line 2')

    # Add labels and title
    plt.xlabel('Year')
    plt.ylabel('Sea Level (inches)')
    plt.title('Rise in Sea Level')

    # Adjust x-axis ticks
    plt.xticks(np.arange(1850, 2100, 25))

    # Save plot and return data for testing (DO NOT MODIFY)
    plt.savefig('sea_level_plot.png')
    return plt.gca()
```

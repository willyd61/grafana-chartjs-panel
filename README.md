## Chart.js Panel Plugin for Grafana

Create bar charts in Grafana using Chart.js.

## Installation

clone this repository into your plugin directory

```
git clone https://github.com/CopperHill-Consulting/grafana-chartjs-panel.git
brew services restart grafana
```

## Drilldown Links
You can add drilldown links to segments.  In addition there are meta groups that can be used to pass time ranges and variables to the drilldown links.

### Time Specific
If you want to copy the same time range values into the drilldown link you can use one of the following:

- `${time}`
   
  This will evaluate to the URL search parameters for `from` and `to`.  For example, if the user selects "Last 5 years" as the time range then `https://example.com/d/ASDFghjkl/test?${time}` will evaluate to `https://example.com/d/ASDFghjkl/test?from=now-5y&to=now`.

- `${time-from}`

  This will evaluate to the URL search parameter for `from`.  For example, if the user selects "Last 6 months" as the time range then `https://example.com/d/ASDFghjkl/test?${time-from}` will evaluate to `https://example.com/d/ASDFghjkl/test?$from=now-5M`.
  
- `${time-to}`

  This will evaluate to the URL search parameter for `from`.  For example, if the user selects "This day last week" as the time range then `https://example.com/d/ASDFghjkl/test?${time-to}` will evaluate to `https://example.com/d/ASDFghjkl/test?$to=now-7d%2Fd`.
  
### Variables
If you want to use the value of variables in drilldown links you can use any of the following meta groups:

- `${var:name_of_variable}`

  Using this format gives you the ability to simply take the value(s) of the specified variable and put it into the drilldown link.  For example if you have a variable called `age` and the value is `25` you can use `https://example.com/d/ASDFghjkl/test?var-age=${var:age}` and `https://example.com/d/ASDFghjkl/test?var-age=25` will be the result.  Another example would be that the `age` variable has the values `25` and `34`.  If you use the same drilldown URL as before the result will be `https://example.com/d/ASDFghjkl/test?var-age=25%2C34` because both values will simply be concatenated by a comma.

- `${var:name_of_variable:param}`

  Using this format gives you the ability to simply take the value(s) of the specified variable and put it into the drilldown link with the name of the variable included.  For example if you have a variable called `age` and the value is `25` you can use `https://example.com/d/ASDFghjkl/test?${var:age:param}` and `https://example.com/d/ASDFghjkl/test?var-age=25` will be the result.  Another example would be that the `age` variable has the values `25` and `34`.  If you use the same drilldown URL as before the result will be `https://example.com/d/ASDFghjkl/test?var-age=25&var-age=34` because it passes each value in separately.
  
  **NOTE:**  If you prefix this meta group with "`var-`" these 4 characters will be ignored.  For example `https://example.com/d/ASDFghjkl/test?var-${var:age:param}` will still evaluate to `https://example.com/d/ASDFghjkl/test?var-age=25` in the case that `age` is `25`.  On the other hand, if you used `https://example.com/d/ASDFghjkl/test?svar-${var:age:param}` it would be evaluated to `https://example.com/d/ASDFghjkl/test?svar-var-age=25`.

- `${var:name_of_variable:param:name-of-url-param}`

  Using this format gives you the ability to simply take the value(s) of the specified variable and put it into the drilldown link with the name of the variable included as you specify.  For example if you have a variable called `age` and the value is `25` you can use `https://example.com/d/ASDFghjkl/test?${var:age:param:edad}` and `https://example.com/d/ASDFghjkl/test?edad=25` will be the result.  Another example would be that the `age` variable has the values `25` and `34`.  If you use the same drilldown URL as before the result will be `https://example.com/d/ASDFghjkl/test?edad=25&edad=34` because it passes each value in separately.

## License
MIT

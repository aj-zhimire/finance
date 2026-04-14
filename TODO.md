# To-Do

## Status

- Completed: pulled `df_trade_daily`, `df_nav`, and `df_rate_daily`
- Completed: built an initial NAV announcement event-window dataset
- In progress: test returns on day `0`, `+1`, and `+2` relative to day `-1`
- Pending: regress event-day returns on `nav_ret`
- Pending: merge `df_rate_daily` into the event dataset and add the 10-year Treasury yield to the model
- Pending: extend the analysis with credit spread

## Current Modeling Plan

- Build the NAV announcement event-window dataset using `df_nav` and `df_trade_daily`, with day `-1` as the baseline and event days `0`, `+1`, and `+2`.
- Test whether returns on day `0`, `+1`, and `+2` differ from the day `-1` baseline to determine whether NAV announcements are associated with price adjustment.
- For any event day that shows adjustment, regress that day’s return on `nav_ret` from `df_nav` to test whether the size and direction of the market move are related to the NAV change.
- Merge `df_rate_daily` into the event dataset.
- Add the 10-year Treasury yield from `df_rate_daily` as a macro variable in the analysis.
- Keep credit spread from `df_rate_daily` available for the next extension.

## Data Sources

- `df_trade_daily`: daily trade and return data
- `df_nav`: quarterly NAV data from balance sheet filings
- `df_rate_daily`: daily 10-year Treasury yield and credit spread data
